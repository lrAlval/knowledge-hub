> An abstraction over **all** types of **memory** that we can allocate in .NET..

![[20231123171537.png]]
# TL;DR
-  not recommended for **async** **workflows**, for that use `Memory<T>
- general use case => ***Parsing*** and ***formatting***.
	- can parse big numbers in string format to string with `ReadOnlySpan<T>

>Traditional methods for allocated block of memory are:
### Managed memory
```cs
byte[] myArray = new byte[100]
```

### Unmanaged memory
- this allocation is **invisible** to the **GC**, since is unmanaged, you are responsible for releasing the memory.
- to allocate memory:
```cs
IntPtr ptr = Marshal.AllocHGlobal(100)
```
- to free memory:
```cs
Marshal.FreeHGlobal(ptr)
```

## Allocation of memory on the stack
> very efficient since both allocation and deallocation are on the stack.

```cs
byte* myArray = stackallock byte[100]
```
-  ***Caveats***
	- can only do it in unsafeguarded.
	- stack is small, allocate too much and can get ***stack overflow exception.***
	- max size for 32 bits => 1 MB
	- max size for 64 bits => 4 MB