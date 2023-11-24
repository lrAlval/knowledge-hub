In .NET, garbage collection (GC) is the process of automatically managing the memory used by a program by reclaiming memory occupied by objects that are no longer in use. There are 2 GC modes:

# TL;DR

- multi-core ? single app in server ? **Server GC**
    - multi-core ? hundreds of **instances** in server ? use **Workstation GC**
- single-core ? multiple app in server ? **Workstation GC**
    - single core ? single app in server ? **Workstation GC**
- multiple instances ? low amount logical CPUs ? **non-concurrent** mode
- few instances ? high amount of logical CPUs ? **concurrent** mode.

### **Trade-offs**

- **Latency vs. Throughput:**
    - Workstation GC and Server GC is the balance between low-latency and high-throughput.
    - **Workstation GC** prioritizes **low-latency** and is suitable for applications where **responsiveness** is crucial.
    - **Server GC** prioritizes **high-throughput** and is more suitable for server **applications** processing a large number of **requests concurrently**.


# Workstation GC

- designed for **client** apps.
- **default GC** flavor for **standalone** apps.
- For **hosted** apps, for example, those hosted by [ASP.NET](http://asp.net/), the host determines the default GC flavor.
- **asynchronous** per core.
- Use **GC generations**, distinguishing between **short-lived** and **long-lived** objects.
- use **single dedicated thread** for **GC**.
- **optimized** for **low-latency** and **responsiveness**,.
- making it suitable for interactive applications where minimizing **pause times** is critical.
- **prioritizes** low-latency and is suitable for applications where responsiveness is crucial
- You have a **UI** or share the machine with other **important process.**
    - These are **typically** applications with a **graphical** user interface (**GUI**), such as **desktop applications**.
- can be **concurrent** or **non-concurrent**.


# GC Concurrency Models

## Concurrent / Background (**Throughput**)

- aim to minimize the impact on the application's **responsiveness** by performing garbage collection **concurrently** with the **application threads.**
- intended for **server applications** that need high **throughput** and **scalability**.
- **recommended** one for docker apps.
- **potentially** longer overall collection time.

## Non-concurrent (Pause time)

- **Stop-the-World (STW)**
    - The non-concurrent GC performs GC by stopping the execution of all **application** threads.
- also known as a "stop-the-world" event. During this time, the garbage collector scans the managed heap for **unreachable** objects and reclaims their memory.
- whenever the **GC** has something to do, it will stop all your **code** , does its job and as the last step it **resumes** all your **threads**.

## General Considerations

- If you're using the environment variables, .NET 6 and later versions standardize on the prefix `DOTNET_` instead of `COMPlus_`. However, the `COMPlus_` prefix will continue to work. If you're using a previous version of the .NET runtime, you should still use the `COMPlus_` prefix, for example, `COMPlus_gcServer`.
- Because GC is **per process**, it rarely ever makes sense to set these configurations at the machine level. For example, you wouldn't want every .**NET** process on a machine to use **server GC** or the same **heap hard** limit.

# ****Performance considerations****

### ****Workstation GC****

- The collection occurs on the **user thread** that triggered the **garbage collection** and remains at the **same priority**.
- Because **user threads** typically run at **normal priority**, the garbage collector (which runs on a normal priority thread) must **compete** with other **threads** for **CPU time**.
    - (Threads that run native code are not suspended on either server or workstation garbage collection.)
- Workstation garbage collection is **always used** on a computer that has only one **logical CPU**, regardless of the config.

### ****Server GC****

**TL;DR**

If you're running **hundreds** of instances of an **application**, consider using **workstation GC** with **concurrent GC disabled**.

This will result in less context **switching**, which can **improve** performance.

- The collection occurs on **multiple** **dedicated** **threads**.
    - On Windows, these threads run at `THREAD_PRIORITY_HIGHEST` priority level.
- A **heap** and a **dedicated thread** to perform garbage collection are provided for **each logical CPU**, and the heaps are collected at the same time.
    - Each **heap** contains a **small object heap** and a **large object heap**, and all heaps can be accessed by user code. Objects on different heaps can refer to each other.
- Because multiple garbage collection threads work together, server garbage collection is faster than workstation garbage collection on the same size heap.
- Server garbage collection often has larger size segments. However, this is only a generalization: segment size is implementation-specific and is subject to change. Don't make assumptions about the size of segments allocated by the garbage collector when tuning your app.
- **Server GC** can be **resource**-**intensive**.
    - For example, imagine that there are 12 processes that use server GC running on a computer that has four **logical CPUs**.
    - If all the processes happen to collect garbage at the same time, they would interfere with each other, as there would be **12** threads **scheduled** on the same **logical CPU**.
    - If the processes are **active**, it's **not** a **good** idea to have them **all use server GC**.


# Interesting Links

- [Workstation vs. server garbage collection (GC) - .NET](https://learn.microsoft.com/en-us/dotnet/standard/garbage-collection/workstation-server-gc)
- [Garbage collector config settings - .NET](https://learn.microsoft.com/en-us/dotnet/core/runtime-config/garbage-collector#flavors-of-garbage-collection)
- [Fundamentals of garbage collection - .NET](https://learn.microsoft.com/en-us/dotnet/standard/garbage-collection/fundamentals)