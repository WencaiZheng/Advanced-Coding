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
re.split('\W+', 'Words, words, words.') // only get english words
re.split('(\W+)', 'Words, words, words.')// split everything
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

## sort the dictionary

```python
sorted(freq.items(), key=lambda x: x[1], reverse=True)
sorted(freq.items(), key=lambda x: x[0], reverse=True)
```

## find prime

```python
def findPrime(N):
    primes=[2]
    for i in range(3,N):
        for j in primes:
            if i%j==0:
                break
        else:
            primes.append(i)
    return primes

def isPrime(N):
    for i in range(2,int(N**0.5)):
        if N%i==0:
            return False
    return True
isPrime(9)
```

## zip

```python
strs=["flower","flow","flight"]
print(list(zip(*strs)))
```

## permutation

```python
def permutation(lst): 
    # If lst is empty then there are no permutations 
    if len(lst) == 0: 
        return [] 
    if len(lst) == 1: 
        return [lst] 
    l = [] 
    # Iterate the input(lst) and calculate the permutation 
    for i in range(len(lst)): 
        m = lst[i] 
        # Extract lst[i] or m from the list.  remLst is 
        remLst = lst[:i] + lst[i+1:] 
        # Generating all permutations where m is first element
        for p in permutation(remLst): 
           l.append([m] + p)

    return l 
x=permutation([1,2,3,4])
```

## 0/1 backpack DP

```python
def backPack(w,lim):
    w=[[0,0]]+w
    m=[[0 for i in range (lim+1)] for j in range(len(w))]

    for i in range(1,len(w)):
        for j in range(1,lim+1):
            if w[i][0]>j:
                m[i][j]=m[i-1][j]
            else:
                m[i][j]=max(m[i-1][j],w[i][1]+m[i-1][j-w[i][0]])
    print(m[len(w)-1][lim])
    return m
w=[[1,1],[2,6],[5,18],[6,22],[7,28]]
backPack(w,11)
```

## typical sort

```python
# merge and quick
def mergeSort(arr):
    lenth=len(arr)
    if lenth<=1:
        return arr
    left=arr[:lenth//2]
    right=arr[lenth//2:]
    sort_l=mergeSort(left)
    sort_r=mergeSort(right)
    i,j,temp=0,0,[]
    while i < len(sort_l) and j< len(sort_r):
        if sort_l[i]<sort_r[j]:
            temp.append(sort_l[i])
            i+=1
        else:
            temp.append(sort_r[j])
            j+=1
    if i==len(sort_l):
        temp+=sort_r[j:]
    elif j == len(sort_r):
        temp+=sort_l[i:]
    return temp

def quickSort(lst):
    if len(lst)==1:
        return lst
    if len(lst)==0:
        return []
    piv=lst[0]
    left,right=[],[]
    for i in lst[1:]:
        if i<piv:
            left.append(i)
        else:
            right.append(i)
    sort_l=quickSort(left)
    sort_r=quickSort(right)
    return sort_l+[piv]+sort_r
# x=quickSort()
arr=[4,2,17,2,100000000,-111111111111]
print(mergeSort(arr))
print(quickSort(arr))
```

## set order

```python
mailto = ['cc', 'bbbb', 'afa', 'sss', 'bbbb', 'cc', 'shafa']
addr_to = list(set(mailto))
print(addr_to)
addr_to.sort(key=mailto.index)
print(addr_to)
"""
['afa', 'bbbb', 'cc', 'sss', 'shafa']
['cc', 'bbbb', 'afa', 'sss', 'shafa']
"""
```

## quick/merge sort

```python
def mergeSort(arr):
    lenth=len(arr)
    if lenth<=1:
        return arr
    left=arr[:lenth//2]
    right=arr[lenth//2:]
    sort_l=mergeSort(left)
    sort_r=mergeSort(right)
    i,j,temp=0,0,[]
    while i < len(sort_l) and j< len(sort_r):
        if left[i]<right[j]:
            temp.append(sort_l[i])
            i+=1
        else:
            temp.append(sort_r[j])
            j+=1
    if i==len(sort_l):
        temp+=sort_r[j:]
    elif j == len(sort_r):
        temp+=sort_l[i:]
    return temp

def quickSort(lst):
    if len(lst)==1:
        return lst
    if len(lst)==0:
        return []
    piv=lst[0]
    left,right=[],[]
    for i in lst[1:]:
        if i<piv:
            left.append(i)
        else:
            right.append(i)
    sort_l=quickSort(left)
    sort_r=quickSort(right)
    return sort_l+[piv]+sort_r
#arr=[3,2,1,0,-1,9]
#print(mergeSort(arr))
```

## find prime

```python
def findPrime(N):
    primes=[2]
    for i in range(3,N):
        is_prime=1
        for j in primes:
            if i%j==0:
                is_prime=0
        if is_prime==1:
            primes.append(i)
    return primes
#print(findPrime(1000))
```

# Fibonacci 

```python
def fib2(max):  
    a, b = 0, 1  
    while a < max:  
        yield a  
        a, b = b, a+b
print(list(fib2(10)))
```

## KMP Algorithm

```python
# Python program for KMP Algorithm 
def KMPSearch(pat, txt): 
    M = len(pat) 
    N = len(txt) 
  
    # create lps[] that will hold the longest prefix suffix  
    # values for pattern 
    lps = [0]*M 
    j = 0 # index for pat[] 
  
    # Preprocess the pattern (calculate lps[] array) 
    computeLPSArray(pat, M, lps) 
  
    i = 0 # index for txt[] 
    while i < N: 
        if pat[j] == txt[i]: 
            i += 1
            j += 1
  
        if j == M: 
            print ("Found pattern at index "+ str(i-j) )
            j = lps[j-1] 
  
        # mismatch after j matches 
        elif i < N and pat[j] != txt[i]: 
            # Do not match lps[0..lps[j-1]] characters, 
            # they will match anyway 
            if j != 0: 
                j = lps[j-1] 
            else: 
                i += 1
```

## longest prefix suffix 

```python
def computeLPSArray(pat, M, lps): 
    len = 0 # length of the previous longest prefix suffix 
  
    lps[0] # lps[0] is always 0 
    i = 1
  
    # the loop calculates lps[i] for i = 1 to M-1 
    while i < M: 
        if pat[i]== pat[len]: 
            len += 1
            lps[i] = len
            i += 1
        else: 
            # This is tricky. Consider the example. 
            # AAACAAAA and i = 7. The idea is similar  
            # to search step. 
            if len != 0: 
                len = lps[len-1] 

                # Also, note that we do not increment i here 
            else: 
                lps[i] = 0
                i += 1
  
#txt,pat = "ABABDABACDABABCABAB", "ABABCABAB" ; KMPSearch(pat, txt) 
```

## BFPRT

```python

def BFPRT(nums, k):
    # QuickSelect idea: AC in 52 ms
    # ---------------------------
    #
    pivot = nums[0]
    left  = [l for l in nums if l < pivot]
    equal = [e for e in nums if e == pivot]
    right = [r for r in nums if r > pivot]

    if k <= len(right):
        return BFPRT(right, k)
    elif (k - len(right)) <= len(equal):
        return equal[0]
    else:
        return BFPRT(left, k - len(right) - len(equal))
#a = list(range(1,11));random.shuffle(a);print(BFPRT(a,5))
```

## remove duplicates

```python
def removeDuplicates(nums) -> int:
    lst=nums[0]
    flag=0
    i=1
    while i < len(nums):
        if nums[i]==lst:
            flag+=1
            if flag>=2:
                del nums[i]
            else: i+=1
        else:
            lst=nums[i]
            i+=1
            flag=0
    return len(nums)
#print(removeDuplicates([1,1,1,2,2,3]))
```

## factor!

```python
def fac(k,z):
    if k<=z:
        return 1
    return k*fac(k-1,z)
#print(fac(3,2))
```

## three sum: leetcode 

```python
def threeSum(nums):
    res = []
    nums.sort()
    for i in range(len(nums)-2):
        if i > 0 and nums[i] == nums[i-1]:
            continue
        l, r = i+1, len(nums)-1
        while l < r:
            s = nums[i] + nums[l] + nums[r]
            if s < 0:
                l +=1 
            elif s > 0:
                r -= 1
            else:
                res.append((nums[i], nums[l], nums[r]))
                while l < r and nums[l] == nums[l+1]:
                    l += 1
                while l < r and nums[r] == nums[r-1]:
                    r -= 1
                l += 1; r -= 1
    return res
nums = [-1, 0, 1, 2, -1, -4]
#threeSum(nums)
```

## dynamic programming: backpack problem

```python
def backPack(w,lim):
    w=[[0,0]]+w
    m=[[0 for i in range (lim+1)] for j in range(len(w))]
    for i in range(1,len(w)):
        for j in range(1,lim+1):
            if w[i][0]>j:
                m[i][j]=m[i-1][j]
            else:
                m[i][j]=max(m[i-1][j],w[i][1]+m[i-1][j-w[i][0]])
    print(m[len(w)-1][lim])
    return m
#w=[[1,1],[2,6],[5,18],[6,22],[7,28]]
#m=backPack(w,5)
```

## permutation

```python
def permutation(lst): 
    # If lst is empty then there are no permutations 
    if len(lst) == 0: 
        return [] 
    if len(lst) == 1: 
        return [lst] 
    l = [] 
    # Iterate the input(lst) and calculate the permutation 
    for i in range(len(lst)): 
       m = lst[i] 
       # Extract lst[i] or m from the list.  remLst is 
       remLst = lst[:i] + lst[i+1:] 
       # Generating all permutations where m is first element
       for p in permutation(remLst): 
           l.append([m] + p)

    return l 
#x=permutation([1,2,3,4])
```

## longest common prefix

```python
def longestCommonPrefix( strs):
  """
  :type strs: List[str]
  :rtype: str
  """
  lcp = ""
  for s in zip(*strs):
      if (s[0],) * len(s) == s:
          lcp += s[0]
      else:
          break
  return lcp
#longestCommonPrefix(["flower","flow","flight"])
```

## get data from database via API

```python
def wrds():
    import wrds as db
    db = wrds.Connection(wrds_username='novenwz')
    # pswd: JessieJiaxunLi19960824
    #x=db.raw_sql('select Price from taq LIMIT 10;', date_cols=['date'])
    print(db.list_libraries())
    print(db.list_tables(library="djones"))
    
def quandl():
    import quandl as qd
    token = "pXAyhrp2yzZRFhQj9J-f"
    mydata = qd.get("CHRIS/CME_ED5", authtoken=token, start_date="2001-12-31", end_date="2005-12-31")
    return mydata

def yahoo():
    # define start and end date
    start_date="2010-09-01"
    end_date="2019-10-23"
    stock_names=pd.read_csv("sp500.csv").iloc[:5,0]
    for i,stock in enumerate(stock_names):
        x=yf.download(stock, start=start_date, end=end_date)
        x.to_csv("C:/Users/wenca/Desktop/"+stock)
        print('The {} out of {} is downloaded.'.format(i,len(stock_names)))
```

## insertion sort

```python
def insertSort(arr):
    lenth=len(arr)
    if lenth<=1:
        return arr
    if lenth==2:
        if arr[0]<arr[1]:return arr
        else:return arr[::-1]
    first,sorted_rest=arr[0],insertSort(arr[1:])
    return biSortedInsert(sorted_rest,first)

def biSortedInsert(arr,tar):
    if len(arr)==0:return[tar]
    if len(arr)==1:
        if arr[0]<=tar:return arr+[tar]
        else:return [tar]+arr
    if arr[0]>=tar:return [tar]+arr
    if arr[-1]<=tar:return arr+[tar]    
    if len(arr)==2:return [arr[0]]+[tar]+[arr[-1]]
    else:
        sort=arr
        sort_idx=list(range(len(sort)))
        while len(sort_idx)>2:
            i=len(sort)//2
            if tar<sort[i]:
                sort=sort[:i+1]
                sort_idx=sort_idx[:i+1]
                i=len(sort)//2
            else:
                sort=sort[i:]
                sort_idx=sort_idx[i:]
                i=len(sort)//2
        posi=sort_idx[1]
        return arr[:posi]+[tar]+arr[posi:]
#nums=[3,2]
#print(insertSort(nums))
```

## distance between string

```python

def minDistance(word1, word2):
    l1, l2 = len(word1)+1, len(word2)+1
    dp = [[0 for _ in range(l2)] for _ in range(l1)]
    for i in range(l1):
        dp[i][0] = i
    for j in range(l2):
        dp[0][j] = j
    for i in range(1, l1):
        for j in range(1, l2):
            dp[i][j] = min(dp[i-1][j]+1, dp[i][j-1]+1, dp[i-1][j-1]+(word1[i-1]!=word2[j-1]))
    return dp[-1][-1]

def minDistance( word1: str, word2: str) -> int:
    l1, l2 = len(word1), len(word2)
    dp = [[-1] * (l2+1) for i in range(l1 + 1)] # 建立2D数组
    return getDistance(word1, word2, dp, l1, l2)

def getDistance( word1, word2, dp, pos1, pos2):
    if pos1 == 0: return pos2 # 其中一个时空串
    if pos2 == 0: return pos1
    if dp[pos1][pos2] >= 0: return dp[pos1][pos2]
    res = 0
    if word1[pos1 - 1] == word2[pos2 - 1]:
        res = getDistance(word1, word2, dp, pos1 - 1, pos2 -1)
    else:
        res = min(getDistance(word1, word2, dp, pos1-1, pos2-1), getDistance(word1, word2, dp, pos1-1, pos2), getDistance(word1, word2, dp, pos1, pos2-1)) + 1
        # + 1: 指 replace/ delete/ insert 1 step
    dp[pos1][pos2] = res
    return res

#word1,word2 = "horse" , "ros"
#print(minDistance(word1,word2))
```

## all subset

```python
def subsets(nums):
    if len(nums)==0:
        return []
    if len(nums)==1:
        return [nums,[]]
    res=[]
    for i in range(len(nums)-1):
        res+=([a+[nums[i]] for a in subsets(nums[i+1:])])
    res+=[[nums[-1]],[]]
    return res
x=[1,2,3]
#print(subsets(x))
```

## spiral matrix

```python
def generateMatrix(n):
    A, lo = [], n*n+1
    while lo > 1:
        lo, hi = lo - len(A), lo
        A = [range(lo, hi)] + list(zip(*A[::-1]))
    return A

def generateMatrix1(n):
    A = [[0] * n for _ in range(n)]
    i, j, di, dj = 0, 0, 0, 1
    for k in range(n*n):
        A[i][j] = k + 1
        if A[(i+di)%n][(j+dj)%n]:
            di, dj = dj, -di
        i += di
        j += dj
    return A
print(generateMatrix1(4))
```

## decorator use

```python
# decorator to calculate duration 
# taken by any function. 
def calculate_time(func): 
      
    # added arguments inside the inner1, 
    # if function takes any arguments, 
    # can be added like this. 
    def inner1(*args, **kwargs): 
  
        # storing time before function execution 
        begin = time.time() 
          
        func(*args, **kwargs) 
  
        # storing time after function execution 
        end = time.time() 
        print("Total time taken in : ", func.__name__, end - begin) 
  
    return inner1 
  
# this can be added to any function present, 
# in this case to calculate a factorial 
@calculate_time
def factorial(num): 
  
    # sleep 2 seconds because it takes very less time 
    # so that you can see the actual difference 
    time.sleep(2) 
    print(math.factorial(num)) 
  
# calling the function. 
factorial(10) 
```

