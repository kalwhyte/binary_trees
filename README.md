0x1D. C - Binary trees
======================

-   By Alexandre Gautier

#### In a nutshell...


Resources
---------

**Read or watch**:

-   [Binary tree](https://alx-intranet.hbtn.io/rltoken/1F2x42-8vUbOmU4L1C1KMg "Binary tree") (*note the first line: `Not to be confused with B-tree.`*)
-   [Data Structure and Algorithms - Tree](https://alx-intranet.hbtn.io/rltoken/QmcTMCkQyrgMjrqoWxYdhw "Data Structure and Algorithms - Tree")
-   [Tree Traversal](https://alx-intranet.hbtn.io/rltoken/nMxoYQdZR_guroan8JeqBQ "Tree Traversal")
-   [Binary Search Tree](https://alx-intranet.hbtn.io/rltoken/qO5dBlMnYJzbaWG3xVpcnQ "Binary Search Tree")
-   [Data structures: Binary Tree](https://alx-intranet.hbtn.io/rltoken/BeyJ2gjlE7_djwRiDyeHig "Data structures: Binary Tree")

Learning Objectives
-------------------

At the end of this project, you are expected to be able to [explain to anyone](https://alx-intranet.hbtn.io/rltoken/rDjGcLNoVZsZG1Br0UbX6A "explain to anyone"), **without the help of Google**:

### General

-   What is a binary tree
-   What is the difference between a binary tree and a Binary Search Tree
-   What is the possible gain in terms of time complexity compared to linked lists
-   What are the depth, the height, the size of a binary tree
-   What are the different traversal methods to go through a binary tree
-   What is a complete, a full, a perfect, a balanced binary tree

Requirements
------------

### General

-   Allowed editors: `vi`, `vim`, `emacs`
-   All your files will be compiled on Ubuntu 20.04 LTS using gcc, using the options -Wall -Werror -Wextra -pedantic -std=gnu89
-   All your files should end with a new line
-   A `README.md` file, at the root of the folder of the project, is mandatory
-   Your code should use the `Betty` style. It will be checked using [betty-style.pl](https://github.com/holbertonschool/Betty/blob/master/betty-style.pl "betty-style.pl") and [betty-doc.pl](https://github.com/holbertonschool/Betty/blob/master/betty-doc.pl "betty-doc.pl")
-   You are not allowed to use global variables
-   No more than 5 functions per file
-   You are allowed to use the standard library
-   In the following examples, the `main.c` files are shown as examples. You can use them to test your functions, but you don't have to push them to your repo (if you do we won't take them into account). We will use our own `main.c` files at compilation. Our `main.c` files might be different from the one shown in the examples
-   The prototypes of all your functions should be included in your header file called `binary_trees.h`
-   Don't forget to push your header file
-   All your header files should be include guarded

### GitHub

**There should be one project repository per group. If you clone/fork/whatever a project repository with the same name before the second deadline, you risk a 0% score.**

More Info
---------

### Data structures

Please use the following data structures and types for binary trees. Don't forget to include them in your header file.

#### Basic Binary Tree

```
/**
 * struct binary_tree_s - Binary tree node
 *
 * @n: Integer stored in the node
 * @parent: Pointer to the parent node
 * @left: Pointer to the left child node
 * @right: Pointer to the right child node
 */
struct binary_tree_s
{
    int n;
    struct binary_tree_s *parent;
    struct binary_tree_s *left;
    struct binary_tree_s *right;
};
typedef struct binary_tree_s binary_tree_t;
```

#### Binary Search Tree

```
typedef struct binary_tree_s bst_t;
```

#### AVL Tree

```
typedef struct binary_tree_s avl_t;
```

#### Max Binary Heap

```
typedef struct binary_tree_s heap_t;
```

**Note:** For tasks 0 to 23 (included), you have to deal with simple binary trees. They are not BSTs, thus they don't follow any kind of rule.

### Print function

To match the examples in the tasks, you are given [this function](https://github.com/holbertonschool/0x1C.c "this function")

This function is used only for visualization purposes. You don't have to push it to your repo. It may not be used during the correction

Tasks
-----

#include <stdlib.h>
#include "binary_trees.h"
/**
 * main - Entry point
 *
 * Return: 0 on success, error code on failure
 */
int main(void)
{
    heap_t *tree;
    int array[] = {
        79, 47, 68, 87, 84, 91, 21, 32, 34, 2,
        20, 22, 98, 1, 62, 95
    };
    size_t n = sizeof(array) / sizeof(array[0]);
    tree = array_to_heap(array, n);
    if (!tree)
        return (1);
    binary_tree_print(tree);
    return (0);
}
alex@/tmp/binary_trees$ gcc -Wall -Wextra -Werror -pedantic binary_tree_print.c 132-main.c 132-array_to_heap.c 131-heap_insert.c 0-binary_tree_node.c -o 132-heap_array
alex@/tmp/binary_trees$ ./132-heap_array
                      .-----------------(098)-----------------.
            .-------(095)-------.                   .-------(091)-------.
       .--(084)--.         .--(079)--.         .--(087)--.         .--(062)--.
  .--(047)     (034)     (002)     (020)     (022)     (068)     (001)     (021)
(032)
alex@/tmp/binary_trees$
```

**Repo:**

-   GitHub repository: `binary_trees`
-   File: `132-array_to_heap.c, 131-heap_insert.c, 0-binary_tree_node.c`

### 39\. Heap - Extract

#advanced


Write a function that extracts the root node of a Max Binary Heap

-   Prototype: `int heap_extract(heap_t **root);`
-   Where `root` is a double pointer to the root node of heap
-   Your function must return the value stored in the root node
-   The root node must be freed and replace with the last `level-order` node of the heap
-   Once replaced, the heap must be rebuilt if necessary
-   If your function fails, return `0`

```
alex@/tmp/binary_trees$ cat 133-main.c
#include <stdlib.h>
#include <stdio.h>
#include "binary_trees.h"
/**
 * main - Entry point
 *
 * Return: 0 on success, error code on failure
 */
int main(void)
{
    heap_t *tree;
    int array[] = {
        79, 47, 68, 87, 84, 91, 21, 32, 34, 2,
        20, 22, 98, 1, 62, 95
    };
    size_t n = sizeof(array) / sizeof(array[0]);
    int extract;
    tree = array_to_heap(array, n);
    if (!tree)
        return (1);
    binary_tree_print(tree);
    extract = heap_extract(&tree);
    printf("Extracted: %d\n", extract);
    binary_tree_print(tree);
    extract = heap_extract(&tree);
    printf("Extracted: %d\n", extract);
    binary_tree_print(tree);
    extract = heap_extract(&tree);
    printf("Extracted: %d\n", extract);
    binary_tree_print(tree);
    binary_tree_delete(tree);
    return (0);
}
alex@/tmp/binary_trees$ gcc -Wall -Wextra -Werror -pedantic binary_tree_print.c 133-main.c 133-heap_extract.c 132-array_to_heap.c 131-heap_insert.c 3-binary_tree_delete.c -o 133-heap_extract
alex@/tmp/binary_trees$ valgrind ./133-heap_extract
==29133== Memcheck, a memory error detector
==29133== Copyright (C) 2002-2013, and GNU GPL'd, by Julian Seward et al.
==29133== Using Valgrind-3.10.1 and LibVEX; rerun with -h for copyright info
==29133== Command: ./133-heap_extract
==29133==
                      .-----------------(098)-----------------.
            .-------(095)-------.                   .-------(091)-------.
       .--(084)--.         .--(079)--.         .--(087)--.         .--(062)--.
  .--(047)     (034)     (002)     (020)     (022)     (068)     (001)     (021)
(032)
Extracted: 98
                 .-----------------(095)-----------------.
       .-------(084)-------.                   .-------(091)-------.
  .--(047)--.         .--(079)--.         .--(087)--.         .--(062)--.
(032)     (034)     (002)     (020)     (022)     (068)     (001)     (021)
Extracted: 95
                 .-----------------(091)-----------------.
       .-------(084)-------.                   .-------(087)-------.
  .--(047)--.         .--(079)--.         .--(068)--.         .--(062)
(032)     (034)     (002)     (020)     (022)     (021)     (001)
Extracted: 91
                 .-----------------(087)-----------------.
       .-------(084)-------.                   .-------(068)--.
  .--(047)--.         .--(079)--.         .--(022)--.       (062)
(032)     (034)     (002)     (020)     (001)     (021)
==29133==
==29133== HEAP SUMMARY:
==29133==     in use at exit: 0 bytes in 0 blocks
==29133==   total heap usage: 213 allocs, 213 frees, 9,063 bytes allocated
==29133==
==29133== All heap blocks were freed -- no leaks are possible
==29133==
==29133== For counts of detected and suppressed errors, rerun with: -v
==29133== ERROR SUMMARY: 0 errors from 0 contexts (suppressed: 0 from 0)
alex@/tmp/binary_trees$
```

**Repo:**

-   GitHub repository: `binary_trees`
-   File: `133-heap_extract.c`

### 40\. Heap - Sort

#advanced


Write a function that converts a Binary Max Heap to a sorted array of integers

-   Prototype: `int *heap_to_sorted_array(heap_t *heap, size_t *size);`
-   Where `heap` is a pointer to the root node of the heap to convert
-   And `size` is an address to store the size of the array
-   You can assume `size` is a valid address
-   Since we are using Max Heap, the returned array must be sorted in descending order

Your file `133-heap_extract.c` will be compile during the correction

```
alex@/tmp/binary_trees$ cat 134-main.c
#include <stdlib.h>
#include <stdio.h>
#include "binary_trees.h"
/**
 * print_array - Prints an array of integers
 *
 * @array: The array to be printed
 * @size: Number of elements in @array
 */
void print_array(const int *array, size_t size)
{
    size_t i;
    i = 0;
    while (array && i < size)
    {
        if (i > 0)
            printf(", ");
        printf("%d", array[i]);
        ++i;
    }
    printf("\n");
}
/**
 * main - Entry point
 *
 * Return: 0 on success, error code on failure
 */
int main(void)
{
    heap_t *tree;
    int array[] = {
        79, 47, 68, 87, 84, 91, 21, 32, 34, 2,
        20, 22, 98, 1, 62, 95
    };
    size_t n = sizeof(array) / sizeof(array[0]);
    int *sorted;
    size_t sorted_size;
    print_array(array, n);
    tree = array_to_heap(array, n);
    if (!tree)
        return (1);
    binary_tree_print(tree);
    sorted = heap_to_sorted_array(tree, &sorted_size);
    print_array(sorted, sorted_size);
    free(sorted);
    return (0);
}
alex@/tmp/binary_trees$ gcc -Wall -Wextra -Werror -pedantic binary_tree_print.c 134-main.c 134-heap_to_sorted_array.c 133-heap_extract.c 132-array_to_heap.c 131-heap_insert.c -o 134-heap_sort
alex@/tmp/binary_trees$ valgrind ./134-heap_sort
==46529== Memcheck, a memory error detector
==46529== Copyright (C) 2002-2013, and GNU GPL'd, by Julian Seward et al.
==46529== Using Valgrind-3.10.1 and LibVEX; rerun with -h for copyright info
==46529== Command: ./134-heap_sort
==46529==
79, 47, 68, 87, 84, 91, 21, 32, 34, 2, 20, 22, 98, 1, 62, 95
                      .-----------------(098)-----------------.
            .-------(095)-------.                   .-------(091)-------.
       .--(084)--.         .--(079)--.         .--(087)--.         .--(062)--.
  .--(047)     (034)     (002)     (020)     (022)     (068)     (001)     (021)
(032)
98, 95, 91, 87, 84, 79, 68, 62, 47, 34, 32, 22, 21, 20, 2, 1
==46529==
==46529== HEAP SUMMARY:
==46529==     in use at exit: 0 bytes in 0 blocks
==46529==   total heap usage: 301 allocs, 301 frees, 8,323 bytes allocated
==46529==
==46529== All heap blocks were freed -- no leaks are possible
==46529==
==46529== For counts of detected and suppressed errors, rerun with: -v
==46529== ERROR SUMMARY: 0 errors from 0 contexts (suppressed: 0 from 0)
alex@/tmp/binary_trees$
```

**Repo:**

-   GitHub repository: `binary_trees`
-   File: `134-heap_to_sorted_array.c, 133-heap_extract.c`

### 41\. Big O #Binary Heap

#advanced


What are the average time complexities of those operations on a Binary Heap (one answer per line):

-   Inserting the value n
-   Extracting the root node
-   Searching for a node in a binary heap of size n

**Repo:**

-   GitHub repository: `binary_trees`
-   File: `135-O`
