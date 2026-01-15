# FastPath: Zero-Copy Asynchronous Logger

**FastPath** is a high-performance, low-latency asynchronous logging framework designed for environments where nanoseconds matter.

The goal of this project is to allow a "Hot Path" thread (e.g., a Trading Engine) to log critical events without being stalled by slow I/O operations or Operating System interrupts.



## Key Features 
- **Lock-Free Concurrency:** Implements a Single-Producer Single-Consumer (SPSC) Ring Buffer using `std::atomic` to eliminate mutex contention and kernel context switches.
- **Cache-Line Alignment:** Utilizes `alignas(64)` to prevent **False Sharing**, ensuring the Producer and Consumer threads operate on independent cache lines.
- **Zero-Allocation Hot Path:** Uses fixed-size binary structures (POD types) instead of `std::string` to avoid non-deterministic heap allocations.
- **Memory Ordering:** Optimized with `memory_order_acquire` and `memory_order_release` semantics for deterministic instruction ordering.



## Tech Stack
- **Language:** C++20
- **Platform:** Linux / WSL2
- **Tools:** GCC/G++, Pthreads, Linux Perf (for cache-miss analysis)
