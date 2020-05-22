# Small python tricks

## list of list transpose

```python
arr=[[1, 2], [3, 4], [5, 6]]
list(map(list,zip(*arr)))
```

## Filter

```python
numbers = (1, 2, 3, 4) 
len(list(filter(lambda x: (x >0), numbers)))
```

## padding

```python
import  numpy as np
def pad_with(vector, pad_width, iaxis, kwargs):
    pad_value = kwargs.get('padder', 10)
    vector[:pad_width[0]] = pad_value
    vector[-pad_width[1]:] = pad_value
np.pad(arr,1,pad_with, padder=0)
```

## string split

```python
import re
re.split('\W+', 'Words, words, words.')
re.split('(\W+)', 'Words, words, words.')
re.split('\W+', 'Words, words, words.', 1)
```

## count frequency in list

```python
mylist=[3,3,3,4,5,6]
freq = {} 
for item in mylist: 
    if (item in freq): 
        freq[item] += 1
    else: 
        freq[item] = 1
```

## sort the dictionary by its values

```python
sorted(freq.items(), key=lambda x: x[1], reverse=True)
```

## sort the dictionary by its keys

```python
sorted(freq.items(), key=lambda x: x[0], reverse=True)
```

