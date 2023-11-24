- don’t **allocate** too much on the **managed heap.**
    - less allocations , means less works for the **GC,** which translate to less **work** for the **CPU.**
- don’t have **GC roots** to objects that we **don’t need**.
- **Pattern matching**:
    - generally is faster, but it should be bench to test to see this 
    
![[Pasted image 20231123170133.png]]

- **ValueTask** discriminated union → Either a **Task** or the result of a task
    - it doesn’t allocate on the **Managed Heap**
    - **caveats:**
        - only use it, if you know the result of the **asynchronous** operation is **immediately available** or when you already have a **cached result.**
        - **Only if performance analysis proves it worthwhile should a `ValueTask<TResult>` be used instead of `Task<TResult>`.**

![[Pasted image 20231123170251.png]]
    
- C# Tuples feature is a **value type**, the old Tuple<K1,K2> is a **reference** Type
    - with the new tuple you **avoid allocations.**
- Use _**local functions**_
    - **Delegates (Func)** **allocate** a new object in the **Managed Heap**

![[Pasted image 20231123170457.png]]


- return **ref** for **value** **types**
    - this is useful when you have a big value type 
	    - e.g array of **ints**, and want to avoid copying all the items whenever you return from the **method**.
    - the **ref** keyword was introduced to avoid the “**unsafe**” keyword.

![[Pasted image 20231123170602.png]]