- This class help reduce extra allocations for **big** arrays
- `ArrayPool<T>` New API from C# 7 to “rent” temp arrays.

![[Pasted image 20231123170917.png]]
![[20231123171537.png]]



Test
![](https://raw.githubusercontent.com/lrAlval/interview-topics/main/attachments/20231123171537.png?token=GHSAT0AAAAAACI5UPJEE54Z4RNIR4DXXTQQZK73JMQ)






## Methods


- Rent an array of size.


```cs
public void TestRent()
{
  var arr = ArrayPool<int>.Shared.Rent(256 * 1024);
  Console.WriteLine(arr[0].ToString());
  //use arr.
  ArrayPool<int>.Shared.Return(arr);
}
```

- Create
	- creates a **custom array** pool bigger than **max default 2^20.**
	- only use custom pools, when strictly **needed** , each custom pool is stored in **Large Object Heap** (**LOH)** so **it means a FULL GC sweep and more CPU work**.