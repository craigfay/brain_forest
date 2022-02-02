# Unikernals

In [[Computer Science]], unikernals are radically lightweight single purpose operating systems. Unlike a general purpose OS which handles configuration at runtime, a unikernal handles configuration at compile time.

## Components
A unikernal only contains **system libraries**, **a language runtime**, and **explicitly included supporting applications**. These components are bundled together to form a single Virtual Machine that can execute on a [[Hypervisor]].

## Benefits
- Uncoupled from vendors
- Less management overhead (compared with containers)
- Security: Because of their drastically reduced surface area, Unikernals are implicitly less vulnerable than other deploy targets.
	- No Remote Shell Access
	- No [Syscalls]([system calls](https://www.geeksforgeeks.org/introduction-of-system-call)). Attackers would need to have complete knowledge of the memory layout to call the OS.
	- No access to Ring O. Unikernals execute in [Kernal Space]([kernel space](https://www.sciencedirect.com/topics/computer-science/kernel-address-space)), because they manage [page tables](https://www.geeksforgeeks.org/page-table-entries-in-page-table/) and virtual hardware. A hypervisor sets up the Virtual Machine before it is loaded and makes [para-virtualized](https://www.sciencedirect.com/topics/computer-science/paravirtualization) interfaces to the hardware, making access to [ring 0](https://www.futurelearn.com/info/courses/computer-systems/0/steps/53514) unnecessary.


## Limitations
As might be expected Unikernals have some fundamental limitations:
- Single process (but multiple threads)
- Single user
- Limited debugging
- Limited library ecosystem

## Security

## MiniOS
[MiniOS](https://wiki.xenproject.org/wiki/Mini-OS-DevNotes) is an OS suitable for use as a unikernal. It is distributed with [[Xen Hypervisor]].

## Solo5
[Solo5](https://github.com/Solo5/solo5) is meant to be an interface platform between a unikernel and the hypervisor. Unlike MiniOS, the target hypervisor is KVM/QEMU rather than Xen Project. Where Xen Project leverages paravirtualization to allow the unikernel to talk to the hypervisor, Solo5 contains a hardware abstraction layer to enable the hardware virtualisation used by its target hypervisors.

## HaLVM
The Haskell Lightweight Virtual Machine, or [HaLVM](https://github.com/GaloisInc/HaLVM), is a port of the Glasgow Haskell Compiler toolsuite to enable developers to write high-level, lightweight virtual machines that can run directly on the Xen hypervisor.

## ClickOS
[ClickOS](http://cnp.neclab.eu/projects/clickos/), a high-performance, virtualised software middlebox platform is a unikernel specialised for Network Function Virtualisation. ClickOS virtual machines are small (5MB), boot quickly (about 30 milliseconds), add little delay (45 microseconds), and over 100 of them can be concurrently run while saturating a 10Gb pipe on a commodity server.

## IncludeOS
[IncludeOS](https://www.includeos.org/) is an operating-system library for building unikernels, written in C++. It can take advantage of multiple CPUs and threads can be used to distribute workload onto multiple CPU cores. It also maintains a limited source-code compatibility with Linux.
