# Algorithm Method

# Array

## union two arrays return as a sorted array

double-pointer: 

1. Get array a[] and b[];
2. If arrays aren't sorted array, sort them first
3. Define two pointer
4. Loop a[] and b[] in the same time
5. Skip duplicate items
6. Union a[] b[] in two result array c[]. Compare every item, and add a smaller one into the c[]. If both item values are equal, adding one of them is ok
7. If a[] b[] have different lengths, handle the remaining items at last
8. Loop the remaining items, deal with duplicate items and the last item 

