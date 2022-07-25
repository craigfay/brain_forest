
## Benchmarking Tools and Standards
- [Yahoo Cloud Serving Benchmark (YCSB)](https://en.wikipedia.org/wiki/YCSB)
- [TCP-C Benchmark](): Focuses on throughput and ACID compliance


## Classifying Databases by their Tradeoffs
- **Hot** (short-term) or **cold** (long-term) data?

- **Big** records or **small** records?
- **Analysis** or **Application**?
	- Analysis databases are optimized for flexible, complex, long-running, ad-hoc queries. Some call refer to these as **OLTP** "Online Transaction Processing" databases.
	- Application databases are optimized for supporting user-facing software. Some refer to these as **OLAP** "Online Analytical Processing" databases.
- **Row** vs. **Column** Oriented: How is data grouped together?
	- **Row orientation** is usually better for **application** use-cases, which consists mostly of **point queries** and **range scans**.
	- **Column orientation** is *sometimes* better for **analytics** uses-cases which involving trend detection, computing averages, etc.., such as finance, sensor monitoring.
	- **Column orientation** usually uses more data, because each field must have a reference to its row. It's possible to avoid this by using offset as an implicit ID.
	- **Column orientation** can exploit vectorized instructions on newer CPUs to process multiplei data-points with a single CPU instruction.
	- **Column orientation** offers inherently better compression ratios. Why? It's all just bytes, after all.
	- [Apache Parquet](), [Apache ORC](), and [RCFile]() are examples of **column-oriented** file formats.
	- [Apache Kudu]() (developed for Hadoop), and [ClickHouse]() are **column-oriented** storage engines.
	- PostgreSQL, MySQL are row-oriented.
	- MonetDB and C-Store are column-oriented.
- **Memory** focused or **disk** focused storage: Where is most of the data stored?
	- Disk-focused databases have to worry about data-layout. 
	- Disk-focused databases almost always have a **page-cache**.
	- Disk-focused databased usually have to have a special strategy variable-sized objects if they want to be space-efficient.
	- Memory-focused databases are more volatile, because most operating systems have horrible hardware isolation, and most memory hardware has asymmetries between read and write latency. See [Non-Volatile Memory]().
	- Memory-focused databases have access to data structures that would be infeasible to store primarily on disk.
	- Memory-focused databases are good for applications that will never exceed a known size. The burdens of disk aren't actually necessary for many use cases.
- **Batch I/O** or **Instant I/O**. This is sometimes called "checkpointing".
- 

# Essential Features
- **Storage Engine**: Contains a serialization scheme, a transaction manager, and file writing strategy. Some implementations require a lock manager.
- **Search Engine**: 
- **Presentation Engine**: Usually contains a query processor, a query optimizer, and the choice of a networking protocol.
- **Execution Engine**: Aggregates the results of local and remote operations.

## Non-Essential Features
- **Sharding Engine**


## Wide Column Stores
Not to be confused with **column-oriented** databases, wide-column stores such as [BigTable]() or [HBase]() represent data as a multi-dimensional map, where columns are grouped into "column families", which usually store data of the same type. These are particularly good for archiving web pages.

## Tombstones
Most modern storage systems do not delete data explicitly. Instead, they use deletion markers ("tombstones"). "Shadowed" data is usually reclaimed during a garbage collection process.

## Data File Implementations
Records almost never have their own file on disk, and are grouped into "pages", where one file contains multiple records. A page can be implemented in several ways:
- **index organized tables**: store records in the index itself, sorted by key, making range scans simple. Storing the index and record together reduces the number of disk seeks.
- **heap organized tables**: usually has data sorted by write-order, which makes writing fast. They require additional primary-index structures to make them searchable. This usually involves an index file that contains the filename and offset for each record.
- **hash organized tables**: records are stored in "buckets". A hashed key determines which bucket a record will belong to. Records in the bucket can be sorted to improve lookup speed. **Git** works this way.

## Index File Implementations
- Primary indexes hold one value per search key.
- Databases have to decide how many layers of indirection they want; How many lookups does it take to retrieve a record from a primary and secondary index key?
	- Does the primary index contain the record?
	- If not, does the secondary index reference the primary key, or the record itself? 
- Secondary indexes may hold several values per search key.
- Indexes can save space by using implicit offsets as references, but have to pay with amortized time when a record is moved or updated. This tends not to work well with write-heavy workloads.

## Storage Structures
Three common variables:
- Use or avoid buffering (batch disk interactions)?
- Mutable or immutable files? immutable strategies include **append-only files** and **copy-on-write**.
- Store values in order or out of order? Storing out of order allows write time optimizations, such as [Bitcask]() and [WiscKey]().

## Binary Search Trees
- The **Balanced Binary Search Tree** has a height of $log_{2}(N)$, where $N$ is the number of items in the tree.
- Without balancing, performance benefits are lost because the structure is determined by insertions and deletions.
- Lookup in an unbalanced tree is $O(N)$ in the worst case, where all items are on one side of the tree (basically a linked list).
- Balancing is done after each insertion, usually by **rotation**. If an insert leaves the tree unbalanced (two consecutive nodes in the branch have only one child), the first node is switched with its parent.
	- `(A) -> (B) -> (C)` becomes `(B) -> (A, C)`
- Because of the frequently updated pointers, and because following multiple pointers on disk is expensive, disk-implementations of B-Trees are impractical.
- On disk, there would be no guarantee that a child would be written close to its parent, because elements are added in random order. This is slightly improved in the case of [Paged Binary Trees]().
- A hypothetically better on-disk data structure would have **high fanout** (children per node) to improve locality of neighboring keys, and **low height** to reduce the number of seeks when following pointers. *This is a description of the B-Tree*.

## Hard Disk Drives
Most traditional algorithms were developed when spinning disks were ubiquitous. Spinning disks increase the cost of random reads, because the read-write head had to move to the desired location. Because head movement is so expensive, there has been an emphasis on organizing data sequentially and compactly on the disk.

The smallest transfer unit of a spinning drive is a sector, so when some operation is performed, at least an entire sector can be read or written. Sector sizes typically range from 512 bytes to 4 Kb.

## Solid State Drives
SSDs are made out of **memory cells** connected into **strings**, typically 32 or 64 cells per string. strings are combined into **arrays**, and arrays into **pages**, pages into **blocks**, blocks into **planes**, planes into **dies**.

- A cell can hold one, or several bits, depending on design. 
- Pages are typically 2-16 Kb.
- Blocks typically contain 2-512 pages.
- The smallest unit that can be written or read is a **page**.
- We can only make changes to empty memory cells, which were erased before the current write.
- The smallest erase-able entity is a **block**.
- Pages in an empty block have to be written **sequentially**.

Flash memory controllers have a **Flash Translation Layer** (FTL) which maps page IDs to physical locations, and tracks which pages are empty, written, and discarded. It is also responsible for **garbage collecting**, which relocates data on partially erased pages so that the page can be erased. 

Since both device types (HDDs and SSDs) address chunks of memory rather than individual byte, most operating systems have a block device abstraction, which hides disk structure and buffers I/O operations internally.

When we read a single word from a block device, the whole block containing it is read. **This is a constraint we cannot ignore.** Writing only full blocks and combining subsequent writes to the same block can reduce the number of I/O operations required. **Buffering** and **immutability** both help achieve this.

Garbage collection can hurt write performance, especially when writes are random and unaligned.

## The Ubiquitous B-Tree
**B-Tree** is an umbrella term for structures that have several properties:
- B-Trees are like binary search trees with more fanout and smaller height.
- B-Trees are sorted, which allows us to logarithmically search for elements.
- Balancing operations (splits and merges) are performed when nodes are full or nearly empty.


We use the nodes of a B-Trees to act as pages of records.

To be precise with language: B-Trees allow storing values on any level: in root, internal, and leaf nodes. **B+-Trees** store values only in leaf nodes; Non-leaf nodes only store keys, and pointers to other nodes.

Since values in B+-Trees are stored only on the leaf level, all operations (inserting, updating, removing, and retrieving data records) affect only leaf nodes and propagate to higher levels only during splits and merges.

Some B-Tree variants also have sibling node pointers, most often on the leaf level, to simplify range scans. These pointers help avoid going back to the parent to find the next sibling. Some implementations have pointers in both directions, forming a double-linked list on the leaf level, which makes the reverse iteration possible.

Unlike Binary Trees, B-Trees are build up from the leaves, instead of down from the root.

## B-Tree Lookup Complexity
Complexity can be viewed from two perspectives: Number of block transfers (seeks) and number of comparisons done during the lookup.

Seeks are $log_{N} \, M$ where $N$ is the number of keys per node, and $M$ is the total number of keys in the tree.

Comarisons are $log_{2} \, M$.

## The B-Tree Lookup Algorithm
To find an item, we must perform a single traversal from root to leaf, aiming to find a searched key or its predecessor. Finding the exact key is used for point queries, updates, and deletions. Predecessors are used for range scans and inserts.

The algorithm starts from the root and performs a binary search, comparing the search key with the keys stored in the root node until it finds the first separator key that is greater than the searched key.

Each time we move down a level of the tree, we narrow the scan range.

**All the data records are stored in the leaves**. The non-leaf nodes only contain pointers.

Each computing device will have its own optimal page size, $k$.


## B-Tree Node Splits
This chapter describes the process used to handle the case where inserts cause overflows in a nodes size.

Non-leaf node splits occur when splits occur below and need to be resolved recursively. When a parents does not have enough space to split, it propogates the split upward, all the way to the root if necessary.

To summarize, node splits are done in four steps:
Allocate a new node.
Copy half the elements from the splitting node to the new one.
Place the new element into the corresponding node.
At the parent of the split node, add a separator key and a pointer to the new node.

## B-Tree Node Merges

Nodes can also underflow, meaning that they need to be redistributed to achieve balance.

To summarize, node merges are done in three steps, assuming the element is already removed:
Copy all elements from the right node to the left one.
Remove the right node pointer from the parent (or demote it in the case of a nonleaf merge).
Remove the right node


**B-Trees are very good on-disk storage structures because they have high fanout and infrequent balancing operations.**


# CHAPTER 3: FILE FORMATS

It is useful to think of on-disk B-Trees as a page management mechanism: algorithms have to compose and navigate pages.

Most of the complexity in B-Trees comes from mutability.

## Motivation

## Binary Encoding

Primitive Types:
- Big Endian vs Little Endian

Strings and Variable Sized Data:
- "Pascal Strings" representent strings as a number that signifies length, followed by the bytes that make up the string. The alternative to Pascal Strings is "null-terminated" strings. Pascal strings are favored because they allow constant time length determination.

Bit Packed Data: Booleans, Enums, and Flags:
- Booleans are usually packed together, 8 per byte whenever possible.
- Packed booleans are sometimes called "flags"

General Principles:
- Files usually start with a fixed-sized "header", and may end with a fixed-sized "trailer".
- The rest of the file usually contains "pages".
- Fixed schema allows reduction of storage footprint, because offsets can be used instead of field names.
- Records often put the fixed-sized fields first, and the variable-sized fields last.

## Page Structure
- Page sizes usually range from 4 - 16 kb.
- Each node occupies one page, or multiple pages linked together.
- "node", "page", and "block" are typically used interchangeably.
- The original B-Tree paper described an structure involving a sequence of triplets (key, value, pointer). This only worked for fixed-sized values, and required relocation when insertions happen anywhere besides the end of the sequence.

## Slotted Pages

When storing variable-sized records, the main problem is **free space management**: Reclaiming the space occupied by removed records.

We can simplify this problem by splitting pages into fixed-sized segments, but this still ends up wasting space because blocks are only partially filled.

**We need a page format that allows us to:
- store variable-sized records with minimal overhead
- reclaim space occupied by the removed records
- reference records in page without regard to their exact location.

**Slotted Page** formats solve this problem by organizing pages into a collection of "slots" or "cells", and splitting pointers and cells into two independent regions on opposite sides of the page. **This means that we only need to reorganize pointers addressing cells to preserve the order, and deleting a record can be done by either nullifying a pointer, or removing it.** 

A slotted page has a fixed-sized header that holds important information about the page and cells. Cells may differ in size, and hold arbitrary data: Keys, pointers, data records, etc..

Many databases use slotted pages, such as PostgreSQL.

Let’s see how this approach fixes the problems we stated in the beginning of this section:
- Minimal overhead: the only overhead incurred by slotted pages is a pointer array holding offsets to the exact positions where the records are stored.
- Space reclamation: space can be reclaimed by defragmenting and rewriting the page.
- Dynamic layout: from outside the page, slots are referenced only by their IDs, so the exact location is internal to the page.

## Cell Layout