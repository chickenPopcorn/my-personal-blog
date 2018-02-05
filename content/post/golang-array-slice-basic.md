---
title: "Golang Array and Slice Basics"
date: 2018-02-04T23:58:50-05:00
draft: false
tags: ["go", "data structure", "array", "slice"]
---

#### Basics in Go Array

There two types of array like data structure in go, array and slice. Array is a **value type** structure with fix length. Zero value for array is zero. See Example Below

```go
package main

import "fmt"

func main() {
    // Example 1: basic syntax
    var arr1 [5]int
    // Zero value for array is zero
    arr2 := [3]int{1, 3, 5}
    arr3 := [...]int{2, 4}
    fmt.Println(arr1, arr2, arr3)
    var grid [4][5]int
    fmt.Println(grid)
    // Prints out
    // [0 0 0 0 0] [1 3 5] [2 4]
    // [[0 0 0 0 0] [0 0 0 0 0] [0 0 0 0 0] [0 0 0 0 0]]
}
```

What's more interesting is array is a **value type** structure with fix length. Different length of arrays, even with same data type, are considered different types of variables(__see example 2.1__). On the other hand variables are past by value in go, which means the contain of an array past in as a parameter, can't be changed from another function. See example below.

```go
package main

import "fmt"

func main() {
    // arr2 := [3]int{1, 3, 5}
    arr3 := [...]int{2, 4}

    // Example 2.1: array is a value type
    // printArray(arr2)
    // error, cant use [3]int as type [2]int
    // [3]int and [2]int are two different data type in go

    // Example 2.2: array is a value type
    mutateArray(arr3)
    fmt.Println(arr3[0])
    // prints 2
    //arr3[0] is not changed
}

func mutateArray(arr [2]int) {
    arr[0] = 100
    // only change arr inside the function
}
```

What we can do in this is case is past in pointer to the array. Remember go converts pointer to variable automatically, so no need to use *arr[0] inside the `mutateArrayPtr` function.

```go
package main

import "fmt"

func main() {
    // arr2 := [3]int{1, 3, 5}
    arr3 := [...]int{2, 4}

    // Example 2.1: array is a value type
    // printArray(arr2)
    // error, cant use [3]int as type [2]int
    // [3]int and [2]int are two different data type in go

    // Example 2.2: array is a value type
    mutateArrayPtr(&arr3)
    fmt.Println(arr3[0])
    // prints 2
    //arr3[0] is not changed
}

func mutateArrayPtr(arr *[2]int) {
    arr[0] = 100
}
```

#### Basics in Go Slice

Slice presents view of underlying array

```go
package main

import "fmt"

func main() {
    // Example 1: basic syntax
    arr1 := [...]int{0, 1, 2, 3, 4}
    arr2 := arr1[:]
    fmt.Println(arr1, arr2)

    // Example 2: slices is a view of underlying array
    muteSlice(arr2)
    fmt.Println(arr2)
    // print [100 1 2 3 4]
}

func muteSlice(arr []int) {
    arr[0] = 100
}
```

Example 1 is the basic usage of slice. Note that zero value for slice is nil. Slice is also extendable. Can you see slice's length vs capacity in example 2. Because when append to slice, its pointer, length and capacity will could change, we need a variable to take take in the return slice after append.

```go
package main

import "fmt"

func main() {
    // Example 1: slice basic
    var slice1 []int
    slice2 := []int{0, 1, 2, 3, 4, 5, 6, 7}
    slice3 := make([]int, 16)
    fmt.Println(slice1, slice2, slice3)

    // Example 2: extending slice
    arr1 := [...]int{0, 1, 2, 3, 4, 5, 6, 7}
    s2 := arr1[1:2]
    s3 := s2[3:4]
    fmt.Println(s2, s3)
    // [0 1 2] [3 4]
    fmt.Printf("s2=%v, len(s2)=%d, cap(s2)=%d\n", s2, len(s2), cap(s2))
    // s2=[1], len(s2)=1, cap(s2)=7
    fmt.Printf("s3=%v, len(s3)=%d, cap(s3)=%d", s3, len(s3), cap(s3))
    // s3=[4], len(s3)=1, cap(s3)=4
}
```

Here is a graphical representation of slice

![slice graphical representation](https://raw.githubusercontent.com/chickenPopcorn/my-personal-blog/master/static/images/slice.png)

A potential __gotta__ of this pointer reference of go is that garbage collection cannot release original array, as it is referenced by other slices. Re-slicing a slice doesn't make a copy of the underlying array. The full array will be kept in memory until it is no longer referenced. Occasionally this can cause inefficiency in memory usage.

For example, this `FindDigits` function loads a file into memory and searches it for the first group of consecutive numeric digits, returning them as a new slice.

```go
var digitRegexp = regexp.MustCompile("[0-9]+")

func FindDigits(filename string) []byte {
    b, _ := ioutil.ReadFile(filename)
    return digitRegexp.Find(b)
}
```

This code behaves as advertised, but the returned []byte points into an array containing the entire file. Since the slice references the original array, as long as the slice is kept around the garbage collector can't release the array; the few useful bytes of the file keep the entire contents in memory.

To fix this problem one can copy the interesting data to a new slice before returning it:

```go
func CopyDigits(filename string) []byte {
    b, _ := ioutil.ReadFile(filename)
    b = digitRegexp.Find(b)
    c := make([]byte, len(b))
    copy(c, b)
    return c
}
```