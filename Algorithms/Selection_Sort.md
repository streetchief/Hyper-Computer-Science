# Selection Sort

## Definition

The selection sort algorithm sorts an array by repeatedly finding the minimum element (considering ascending order) from unsorted part and putting it at the beginning. The algorithm maintains two subarrays in a given array.

1. The subarray which is already sorted.
2. Remaining subarray which is unsorted.

In every iteration of selection sort, the minimum element (considering ascending order) from the unsorted subarray is picked and moved to the sorted subarray.

[Wikipedia Entry](https://en.wikipedia.org/wiki/Selection_sort)

[GeeksForGeeks Entry](https://www.geeksforgeeks.org/selection-sort/)

## Key points

### Advantages

### Disadvantages

## Additional Information

## PsuedoCode

1. Store the first element as the smallest value you've seen so far.
2. Compare this item to the next item in the array until you find a smaller number.
3. If a smaller number is found, designate that smaller number to be the new "minimum" and continue until the end of the array.
4. If the "minimum" is not the value (index) you initially began with, swap the two values.
5. Repeat this with the next element until the array is sorted.

## Implementation

<details>
<summary>Javascript Implementation</summary>

```
function selectionSort(arr) {
  const  length = arr.length;

for (let anchor = 0; anchor < length; ++anchor) {
    let minVal = arr[anchor];
    let indexOfMin = anchor;
    let needSwap = false;

        for (let i = anchor; i < length; i++) {
        if (arr[i] < minVal) {
            indexOfMin = i;
            minVal = arr[i];
            needSwap = true;
        }
        }

        if (needSwap) {
        arr[indexOfMin] = arr[anchor];
        arr[anchor] = minVal;
        needSwap = false;
        }

    }
}
```

</details>
