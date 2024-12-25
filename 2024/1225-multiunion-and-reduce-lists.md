# 1225-multiunion and reduce lists

```python
def reduce_lists(lists):
    # Sort lists by length in descending order to prioritize longer lists
    sorted_lists = sorted(lists, key=len, reverse=True)

    # Store the final result
    result = []

    for current_list in sorted_lists:
        # Check if this list is already a subset of any list in the result
        if not any(set(current_list).issubset(set(existing_list)) for existing_list in result):
            result.append(current_list)

    return result
```

```python
import numpy as np

def multi_union1d(arrays):
    result = arrays[0]
    for arr in arrays[1:]:
        result = np.union1d(result, arr)
    return result

# Usage
arr1 = np.array([1, 2, 3])
arr2 = np.array([3, 4, 5])
arr3 = np.array([5, 6, 7])
arr4 = np.array([7, 8, 9])

arrays = [arr1, arr2, arr3, arr4]
union_result = multi_union1d(arrays)

```

TODO

remember to add different situation of point sources.
