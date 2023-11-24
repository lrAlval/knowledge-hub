- objects can be stored on the Managed **Heap** or **stack:**
    - **Managed heap**: reference types
    - **stack**: **value** types

![[Pasted image 20231123165008.png]]


## Troubleshoot tips

- First identify the type that allocate more and then identify in which method.
- GC runs every once in a while and checks for dead objects (objects with no **GC root reference**)
- Utilization Heap size, physical memory size
- Number of objects
- Typical problems:
    - too much work by the **GC** (hurts CPU)
    - not enough work by the **CG** (eventually out of memory)


### Stack

- store on the **stack** , which means 
	- **less** **allocations**.
	- less **pressure** on the **GC**.
- good for small **types.**
- even better if you use them as **local variables**
- **not always** stored on stack 
	- (**edge case**, if **Object root** is stored in the **heap** , then it will also be stored on the **heap**).
- implement ****IEquatable**** and override **Equals**:
	- default implementation has **unboxing** and **decreases performance**.
- in case of big value types: value **semantic** ⇒ it will be copied


### Managed Heap

- Small object Heap (**SOH**) : objects < **85** k bytes:
    - **Gen0** 👶 ****:
        - ***very frequently - fast collection***
        - new objects are placed here, most will be collected on first **sweep**.
    - **Gen1** 👨‍🎓 ****:
        - ***less frequently***
        - Include **gen0** sweep.
        - **Survivors** of the first sweep are placed **here**, **buffer** between **Gen0** and **Gen2.**
    - **Gen2** 👴 ****:
        - **collected rarely** - ***slower of all three***
        - **Gen2** sweep include **Gen0** and **Gen1** sweep - also called **FULL GC**
        - Survivors of the second sweep are placed here, 
	        - Long living objects 
	        - e.g static fields.
- Large object Heap (**LOH**) : objects > 85 k bytes
    - ***it doesn’t have gens*** , but is collected with **gen2** sweeps.
