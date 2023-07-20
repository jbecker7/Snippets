```python
class findTarget:        

#Lol I forgot the built-in absolute value syntax, so I wrote my own
    def av(self, a, b):

        if a < b :

            return b-a

        return a-b 

    def findImpl(self, arr, low, high, target, closest):

        #base case.

        if low > high:

            return closest
  
        mid = low+(high-low)//2

        if arr[mid] == target:

            return mid

        elif arr[mid] > target:

            if av(mid, target) < closest:

                closest = mid

            return findImpl(arr, low, mid-1, target, closest)

        else:

            if av(mid, target) < closest:

                closest = mid

            return findImpl(arr, mid+1, high, target, closest)


    # return the index of the target in the array. or return -1.

    def find(self, arr: [Int], target):

        return findImpl(arr, 0, len(arr)-1, target,9999999999999999)

```