# `SegmentStack`

A FIFO stack that holds a location in a module tree. 

In this class, the true stack is store in `stack` while the three other arrays `modules`, `module_types`, and `selections` hold the names of the respective segment types in the same order as `stack`. When reading from the stack, get the type at the top of `stack` then read the last element of the respective type array.

## Attributes

`modules : List[str]`
> The list of modules in order of `stack`.

`module_types : List[str]`
> The list of module types in order of `stack`.

`sections : List[str]`
> The list of sections in order of `stack`

`stack : List[SegmentType]` [SegmentType](./SegmentType.md)
> The list representing this stack data structure.

`__current : int`
> The current element consider to be the top of the stack.


## Operations

```python
__init__(self)
```
> Creates a new SegmentStack instance and initializes all list attributes to empty.

```python
push(self, name: str, type: SegmentType) -> None
```
> Pushes the provided segment to the stack.
> 
> `name : str`
> > Name of the segment to add.
> 
> `type : SegmentType` [SegmentType](./SegmentType.md)
> > Type of the segment to add.

```python
pop(self) -> None
```
> Pops the current segment from the stack.

```python
go_forward(self, name: str) -> None
```
> Navigates forward through the stack while maintaining the stacks previous order.
Re adds the previous segment type after the current top of the stack.
> 
> `name : str`
> > Name of the segment to add.

```python
go_back(self) -> None
```
> Navigates backward through the stack without permanently modifying it.

```python
__match_apply(self, type: SegmentType, operation: Callable, *args: Any) -> None
```
> Helper method to apply list operations on to each segment depending on the segment type.
> 
> `type : SegmentType` [SegmentType](./SegmentType.md)
> > Type of the segment.
> 
> `operation : Callable`
> > Function to call using the corresponding segment storage and `*args`.
> 
> `*args : Any`
> > Arguments to pass into operation.
