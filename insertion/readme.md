# Insertion Sort

> An insertion sort works by separating an array into two sections, a sorted section and an unsorted section. Initially, of course, the entire array is unsorted. The sorted section is then considered to be empty. The first step is to add a value to the sorted section, so the first item in the array is used (a list of one item is always sorted). Then at each item in the unsorted section:

1. If the item value goes after the last item in the sorted section, then do nothing.
1. If the item value goes before the last item in the sorted section, remove the item value from the array and shift the last sorted item into the now-vacant spot.
1. Compare the item value to the previous value (second to last) in the sorted section.
1. If the item value goes after the previous value and before the last value, then place the item into the open spot between them, otherwise, continue this process until the start of the array is reached.

```js
function insertionSort(items) {

    var len     = items.length,     // number of items in the array
        value,                      // the value currently being compared
        i,                          // index into unsorted section
        j;                          // index into sorted section

    for (i=0; i < len; i++) {

        // store the current value because it may shift later
        value = items[i];

        /*
         * Whenever the value in the sorted section is greater than the value
         * in the unsorted section, shift all items in the sorted section over
         * by one. This creates space in which to insert the value.
         */
        for (j=i-1; j > -1 &#038;&#038; items[j] > value; j--) {
            items[j+1] = items[j];
        }

        items[j+1] = value;
    }

    return items;
}
```

(Source)[https://www.nczonline.net/blog/2012/09/17/computer-science-in-javascript-insertion-sort/]