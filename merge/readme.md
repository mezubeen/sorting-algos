# Merge Sort

### Pseudo Code:

1. If the list is of length 0 or 1, then it is already sorted. Otherwise:
1. Divide the unsorted list into two sublists of about half the size.
1. Sort each sublist recursively by re-applying merge sort.
1. Merge the two sublists back into one sorted list.

![Merge Sort](./merge.png)

```js
var a = [34, 203, 3, 746, 200, 984, 198, 764, 9];
 
function mergeSort(arr)
{
    if (arr.length < 2)
        return arr;
 
    var middle = parseInt(arr.length / 2);
    var left   = arr.slice(0, middle);
    var right  = arr.slice(middle, arr.length);
 
    return merge(mergeSort(left), mergeSort(right));
}
 
function merge(left, right)
{
    var result = [];
 
    while (left.length && right.length) {
        if (left[0] <= right[0]) {
            result.push(left.shift());
        } else {
            result.push(right.shift());
        }
    }
 
    while (left.length)
        result.push(left.shift());
 
    while (right.length)
        result.push(right.shift());
 
    return result;
}
 
console.log(mergeSort(a));
```

[Source 1](https://en.wikipedia.org/wiki/Merge_sort)

[Source 2](http://www.stoimen.com/blog/2010/07/02/friday-algorithms-javascript-merge-sort/)