---
title: openmp | Parallel Program for Two Array's Element Addition
published: 2022-01-19T14:34:00
updated: 2022-01-19T14:34:00
tags: ["parallel algorithms", "openmp"]
---

## Introduction

In this tutorial, we will learn how to implement parallel programming in C using OpenMP.

The program will add two arrays of integers and store the result in another array.

While the program is running, we will print the sum of elements in the array corresponding to that thread id.

## Prerequisites

You need to have gcc installed on your system.

To check if gcc is installed, run the following command:

```bash
gcc --version
```

if you get this error message:

'gcc' is not recognized as an internal or external command,
operable program or batch file.

Then you need to install gcc on your system which you can easily do by following this [windows gcc installation tutorial](https://study-site.anreddy.in/cse/installation-guides/setting-up-vs-code-for-c-cpp-development/)

## Writing a parallel program in C

To write a parallel program in C, we need to use the OpenMP library.

So let's start by including the OpenMP header file.

```c
// Include the OpenMP header file
#include <omp.h>
```

we will use the following pragma directive to enable parallel programming in the program:

```c
#pragma omp parallel num_threads(5)
{
    // Print the thread id
    printf("Thread id: %d\n", omp_get_thread_num());
}
```

Using the pragma directive `num_threads()` option, we can specify the number of threads that will be used to run the program.

The code inside the pragma directive will be forked and executed by each thread in parallel.

We can get the thread id of each thread by using the `omp_get_thread_num()` function.

The thread id of the original thread will be 0. The thread id of the first child thread will be 1 and so on. The thread id of the last child thread will be `num_threads() - 1`.

## C program for two array's element addition using OpenMP library

```c
#include <stdio.h>
#include <omp.h>
void main()
{
    int arr1[5] = {1, 2, 3, 4, 5};
    int arr2[5] = {6, 7, 8, 9, 10};
    int result[5];
    int tid;
#pragma omp parallel num_threads(5)
    {
        tid = omp_get_thread_num();
        result[tid] = arr1[tid] + arr2[tid];
        printf("result[%d] = %d\n", tid, result[tid]);
    }
}
```

## Compiling and running the C program using gcc

To compile a c program that is using OpenMP library, we need to use the `-fopenmp` flag. The `-fopenmp` flag is used to enable OpenMP support in the compiler.

Type the following command to compile the program using gcc:

```
gcc -fopenmp file.c
```

file is the name of the c file which we want to compile.

To run the compiled program, type the following command:

```
./a.out
```

## output

You will get a output similar to the following:

```
result[3] = 13
result[4] = 15
result[2] = 11
result[0] = 7
result[1] = 9
```

If you can run the program multiple times, you can notice that the order of
the output is different each time. This is because the threads are executed in
parallel. And the order of execution is not guaranteed to be same each time.
