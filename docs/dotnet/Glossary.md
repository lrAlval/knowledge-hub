
## GC root
- Every object tree must have one or more root objects.
- As long as the application can reach those roots, the whole tree is reachable.
- But when are those root objects considered reachable? Special objects called garbage-collection roots (GC roots; see Figure below) are always reachable and so is any object that has a garbage-collection root at its own root.

![[Pasted image 20231123170739.png]]
