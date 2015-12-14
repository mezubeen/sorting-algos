# Sorting Algorithms

## Warm Up:
#### Implement Bubble Sort in JavaScript.

> Bubble sort is a sorting algorithm that works by repeatedly stepping through lists that need to be sorted, comparing each pair of adjacent items and swapping them if they are in the wrong order. This passing procedure is repeated until no swaps are required, indicating that the list is sorted. Bubble sort gets its name because smaller elements bubble toward the top of the list.

> Bubble sort is also referred to as sinking sort or comparison sort.

[Source](https://www.techopedia.com/definition/3757/bubble-sort)

**Pseudo code:**

1. Compare the first item to the second item.
1. If the first item should be after the second item, swap them.
1. Compare the second item to the third item.
1. If the second item should be after the third item, swap them.
1. Continue until the end of the data set is reached.

[Source](https://www.nczonline.net/blog/2009/05/26/computer-science-in-javascript-bubble-sort/)

# Morning Lecture
###  Selection Sort

The selection sort algorithm, similar to Bubble Sort in that it shares O(n²) complexity, augments the Bubble Sort algorithm slightly. Instead of comparing each array item to its neighbor, the goal is to locate the *smallest* remaining value and drop it into the correct place in the array. The basic algorithm looks like this:

**Pseudo code:**

1. Assume the first item is the smallest value (minimum).
1. Compare this item to the second item.
1. If the second item is smaller than the first, set the second item as the new minimum.
1. Continue until you reach the end of the array.
1. If the minimum value (index) is not the item (index) you started with, swap them.

[Source](https://www.nczonline.net/blog/2009/09/08/computer-science-in-javascript-selection-sort/)

#### [Practice with this interactive card game](https://www.khanacademy.org/computing/computer-science/algorithms/sorting-algorithms/a/sorting)

We'll need two functions, one to handle our swapping, and one to handle the rest of the sorting logic.

The swap function looks like this:
```js
function swap(arr, a, b) {
    var temp = arr[a];
    arr[a] = arr[b];
    arr[b] = temp;
}
```
The sorting logic is as follows:
```js
function selectionSort(arr) {
    // declare variable min to be used later
    var min;
    // loop through array
    for (var i = 0; i < arr.length; i++) {
        // set min to i for each iteration
        min = i;
        // loop through array, one item ahead of i, for value comparisons
        for (var j = i + 1; j < arr.length; j++) {
            // if any of the items are less than the current min item
            // set min equal to that new item's index
            if (arr[j] < arr[min]) {
                min = j;
            }
        }
        // if the current i no longer equals min, then min must be smaller
        // therefore we swap i with min
        if (i !== min) {
            swap(arr, i, min);
        }
    }
    // when outer loop completes, return the array
    return arr;
}
```
# Afternoon Lecture
## Quick Sort
> Quicksort is a divide and conquer algorithm in the style of merge sort. The basic idea is to find a “pivot” item in the array to compare all other items against, then shift items such that all of the items before the pivot are less than the pivot value and all the items after the pivot are greater than the pivot value. After that, recursively perform the same operation on the items before and after the pivot.

> There are two basic operations in the algorithm, swapping items in place and partitioning a section of the array. The basic steps to partition an array are:

**Pseudo code:**

1. Find a “pivot” item in the array. This item is the basis for comparison for a single round.
1. Start a pointer (the left pointer) at the first item in the array.
1. Start a pointer (the right pointer) at the last item in the array.
1. While the value at the left pointer in the array is less than the pivot value, move the left pointer to the right (add 1). Continue until the value at the left pointer is greater than or equal to the pivot value.
1. While the value at the right pointer in the array is greater than the pivot value, move the right pointer to the left (subtract 1). Continue until the value at the right pointer is less than or equal to the pivot value.
1. If the left pointer is less than or equal to the right pointer, then swap the values at these locations in the array.
1. Move the left pointer to the right by one and the right pointer to the left by one.
1. If the left pointer and right pointer don’t meet, go to step 1.

**The swap function is the same as the one used by Bubble and Selection sort (see above).**

Here is one way to partition the array:
```js
function partition(items, left, right) {
    // find and assign pivot by halving sum of right and left index
    var pivot = items[Math.floor((right + left) / 2)],
        i     = left,
        j     = right;
    // loop until the pointers pass one another
    while (i <= j) {
        // increment i while item[i] is less than pivot
        while (items[i] < pivot) {
            i++;
        }
        // decrement j while item[j] is more than pivot
        while (items[j] > pivot) {
            j--;
        }
        // swap i and j when i is less than or equal to j
        // increment and decrement i and j, respectively
        if (i <= j) {
            swap(items, i, j);
            i++;
            j--;
        }
    }
    // return i to be used as index for recursive calls in quickSort function
    return i;
}
```
And finally, here's the implementation for quick sort, which uses both the partition and swap functions:
```js
function quickSort(items, left, right) {
    // declare index to be used later when each partition returns 'i'
    var index;
    // if statement to handle the base case (any array smaller
    // than length of 1 is returned
    if (items.length > 1) {
        // if no left or right is entered, set them to first and last indeces in array
        left = typeof left != "number" ? 0 : left;
        right = typeof right != "number" ? items.length - 1 : right;
        // set index to return value of partition function
        index = partition(items, left, right);
        // compare current left value to index - 1
        // if left is smaller, then there are still items to be sorted on
        // the left side of the array, so quicksort is called recursively
        if (left < index - 1) {
            quickSort(items, left, index - 1);
        }
        // compare current right value to index
        // if index is smaller than right, then there are still items
        // to be sorted on the right side of the array, so quicksort
        // is called recursively
        if (index < right) {
            quickSort(items, index, right);
        }

    }
    // all recursive calls have finished so the sorted array is returned
    return items;
}
```
[Source](https://www.nczonline.net/blog/2012/11/27/computer-science-in-javascript-quicksort/)
