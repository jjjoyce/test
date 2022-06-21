### 1. Two Sum

Given an array of integers *nums* and an integer *target*, return indices of the two numbers such that they add up to *target*.

You may assume that each input would have **exactly one solution**, and you may not use the same element twice.

You can return the answer in any order.

---

# Brute Force

Enumerate all combinations of two nums

Python:
```python
def twoSum(self, nums, target):
	for i in range(len(nums)):
		for j in range(i+1,len(nums)):
			if nums[i]+nums[j] == target:
				return(i,j)
```

Time complexity $O(n^2)$, Space complexity $O(1)$

# Hash map/Dictionary, trading space for time

Usa a dictionary to record `comp[y]=ind of x`, where $x+y=target$

Python: 
```python
def twoSum(self, nums: List[int], target: int) -> List[int]:
    comp = {}
    for i,n in enumerate(nums):
        if n in comp:
            return [comp[n],i]
        else:
            comp[target-n]=i
    return []
```

C++:
```cpp
public:
    vector<int> twoSum(vector<int>& nums, int target) {
    unordered_map<int, int> comp;

    for (int i=0;i<nums.size();i++) {
        if (comp.find(target-nums[i]) != comp.end()) 
        	return {comp[target - nums[i]], i};
        else comp[nums[i]] = i;
    }

    return {};
}
```
Time complexity $O(n)$, Space complexity $O(n)$

# Two pointer

Apply two pointer on sorted array

Python:
```python
def twoSum(self, nums, target):
	
	nums = enumerate(nums)
	nums = sorted(nums,key = lambda x:x[1])
	l, r = 0, len(nums)-1
	while l<r:
		if nums[l][1]+nums[r][1] == target:
			return [nums[l][0],nums[r][0]]
		elif nums[l][1]+nums[r][1] > target:
			r-=1
		elif nums[l][1]+nums[r][1] < target:
			l+=1
```

C++:
```cpp
public:
    vector<int> twoSum(vector<int>& nums, int target) {
    
    vector<pair<int,int>> numpair;

    for(int i=0;i<nums.size();i++)
            numpair.push_back({nums[i],i});

    sort(numpair.begin(),numpair.end());

    int l=0;
    int r=nums.size()-1;

    while (l<r)
        if (numpair[l].first+numpair[r].first == target)
            return {numpair[l].second, numpair[r].second};
        else if (numpair[l].first+numpair[r].first < target)
            l++;
        else
            r--;

    return {};
}
```

Time complexity $O(n\log n)$, Space complexity $O(n)$. 
(Time require for sorting is $O(n\log n)$)

