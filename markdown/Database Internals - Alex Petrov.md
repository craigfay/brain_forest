
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

## The All Important B-Tree
- The *balanced* tree has a height of $log_{2}(N)$, where $N$ is the number of items in the tree.
- Without balancing, performance benefits are lost because the structure is determined by insertions and deletions.
- Lookup in an unbalanced tree is $O(N)$ in the worst case, where all items are on one side of the tree (basically a linked list).
- Balancing is done after each insertion, usually by **rotation**. If an insert leaves the tree unbalanced (two consecutive nodes in the branch have only one child), the first node is switched with its parent.
	- `(A) -> (B) -> (C)` becomes `(B) -> (A, C)`
- Because of the frequently updated pointers, and because following multiple pointers on disk is expensive, disk-implementations of B-Trees are impractical.
- On disk, there would be no guarantee that a child would be written close to its parent, because elements are added in random order. This is slightly improved in the case of [Paged Binary Trees]().
- A hypothetically better on-disk data structure would have **high fanout** (children per node) to improve locality of neighboring keys, and **low height** to reduce the number of seeks when following pointers.

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




