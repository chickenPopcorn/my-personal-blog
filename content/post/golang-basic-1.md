---
title: "Golang Array Basics 1"
date: 2018-02-04T23:58:50-05:00
draft: false
tags: ["go", "data structure", basic]
---

#### Basics in Go Array and Slice

There two types of array like data structure in go, array and slice. Array is a **value type** structure with fix length. See Example Below

```go
package main

import "fmt"

func main() {
    // Example 1: basic syntax
    var arr1 [5]int
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
