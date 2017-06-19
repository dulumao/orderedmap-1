# OrderedMap [![Build Status](https://travis-ci.org/secnot/orderedmap.svg?branch=master)](https://travis-ci.org/secnot/orderedmap)

OrderedMap is a Go implentation of Python's OrderedDict class, a map that preserves 
the order of insertion, so key:value pairs can be iterated in order they where added

## Installing

Install the package from command line with the following command

```bash
go get -u github.com/secnot/orderedmap
```

And then import in your source file

```go
import "github.com/secnot/orderedmap"
```


## Usage


Basic operations

```go
// Create
om := NewOrderedMap()

// Insert
om.Set("John Smith", 44)
om.Set("Laura Paro", 39)
om.Set("Alison Rogers", 52)

// Update
om.Set("Alison Rogers", 51)

// Get 
if age, ok := om.Get("John Smith"); ok {
	fmt.Printf("John Smith age: %v", age)
}

// Get the last key added
if name, age, ok := om.GetLast() {
	fmt.Printf("%v age: %v\n", name, age)
}

// Delete
om.Delete("John Smith")
```

Iterate over the Map elements in insertion order

```go
om := NewOrderedMap()

om.Set("John Smith", 44)
om.Set("Laura Paro", 39)
om.Set("Alison Rogers", 52)

// Iterate
iter := om.Iter()
for key, value, ok := iter.Next(); ok; key, value, ok := iter.Next() {
	fmt.Printf("%v: %v", key, value)
}

// > Alison Rogers: 52
// > Laura Paro: 39
// > John Smith: 44
```

Pop the last key from the map

```go
key, value, ok := om.PopLast()
// > Alison, 52, true
```

## Documentation


## TYPE

type OrderedMap struct {
	// contains filtered or unexported fields
}

#### func NewOrderedMap

```go
func NewOrderedMap() *OrderedMap
```
Create an empty OrderedMap


#### func (*OrderedMap) Delete

```go
func (*OrderedMap) Delete(key interface{})
```
Delete a key:value pair from the map.


#### func (*OrderedMap) Get

```go
func (om *OrderedMap) Get(key interface{}) (value interface{}, ok bool)
```
Get the value of an existing key, leaving the map unchanged


#### func (om *OrderedMap) GetFirst

```go
func (om *OrderedMap) GetFirst() (key interface{}, value interface{}, ok bool)
```
Get the key value for the beginning element, leaving the map unchanged


#### func (om *OrderedMap) GetLast

```go
func (om *OrderedMap) GetLast() (key interface{}, value interface{}, ok bool)
```
Get the key and value for the last element added, leaving the map
unchanged


#### func (om *OrderedMap) Iter

```go	
func (om *OrderedMap) Iter() *MapIterator
```    
Create a map iterator


#### func (om *OrderedMap) IterReverse

```go
func (om *OrderedMap) IterReverse() *MapIterator
```
Create a reverse ordered map iterator


#### func (om *OrderedMap) Len

```go
func (om *OrderedMap) Len() int
```
Len computes the number of elements in an OrderedMap


#### func (om *OrderedMap) Move

```go
func (om *OrderedMap) Move(key interface{}, last bool) (ok bool)
```
Move an existing key to either the end of the OrderedMap


#### func (om *OrderedMap) MoveFirst

```go
func (om *OrderedMap) MoveFirst(key interface{}) (ok bool)
```
Shortcut to Move an element to the beginning


#### func (om *OrderedMap) MoveLast

```go
func (om *OrderedMap) MoveLast(key interface{}) (ok bool)
```
Shortcut to Move an element to the end


#### func (om *OrderedMap) Pop

```go
func (om *OrderedMap) Pop(last bool) (key interface{}, value interface{}, ok bool)
```

Pop and return key:value for the newest or oldest element on the OrderedMap.


#### func (om *OrderedMap) PopFirst

```go
func (om *OrderedMap) PopFirst() (key interface{}, value interface{}, ok bool)
```

Shortcut to Pop the first element


#### func (om *OrderedMap) PopLast

```go
func (om *OrderedMap) PopLast() (key interface{}, value interface{}, ok bool)
```
Shortcut to Pop the last element


#### func (om *OrderedMap) Set

```go
func (om *OrderedMap) Set(key interface{}, value interface{})
```
Sets the key value, if the key exists it overwrites the existing entry, and
the original insertion position is left unchanged, otherwise the key is
inserted at the end.


## func (om *OrderedMap) String 

```go
func (om *OrderedMap) String() string
```
Stringer interface


## Type

type MapIterator struct {
	// contains filtered or unexported fields
}


#### func (mi *MapIterator) Next

```go
func (mi *MapIterator) Next() (key interface{}, value interface{}, ok bool)
```    
Return iterators next key:value pair


