```c++

/**
* Given an array of integers, return indices of the two numbers such that they add up to a specific target.
* You may assume that each input would have exactly one solution, and you may not use the same element twice.
* Example:
* Given nums = [2, 7, 11, 15], target = 9,
* Because nums[0] + nums[1] = 2 + 7 = 9,
* return [0, 1].
* @param nums
* @param target
* @return
*/


#include <iostream>
#include <vector>
#include <algorithm>
#include <map>

using namespace std;

//暴力搜索
//596 ms 9m
//class SolutionViolence
//{
//public:
	//vector<int> twoSum(vector<int>& nums, int targe)
	//{
	//	vector<int> retTar = {};

	//	for (int i = 0; i < nums.size(); ++i)
	//	{
	//		for (int j = i + 1; j < nums.size(); ++j)
	//		{
	//			if (nums[i] + nums[j] == targe)
	//			{
	//				retTar.push_back(i);
	//				retTar.push_back(j);//不能采用nums[0], JS中可以采用此方法来插入, 但是C++不允许, 因为未申请空间
	//			}
	//		}
	//	}

	//	return retTar;		
	//}
//
//};


//16m 10m
//class Solution {
//public:
//	vector<int> twoSum(vector<int>& nums, int targe)
//	{
//		vector<int> retTar = {};
//		map<int, int> hashTable;
//		for (int i = 0; i < nums.size(); ++i)
//		{
//			int m_sch = targe - nums[i];
//			if (hashTable.count(m_sch))
//			{
//				retTar.push_back(hashTable[m_sch]);
//				retTar.push_back(i);
//				break;
//
//			}
//			hashTable[nums[i]] = i;
//		}
//
//		return retTar;
//	}
//};

//12 ms 10.1m
class Solution {
public:
	vector<int> twoSum(vector<int>& nums, int targe)
	{
		vector<int> retTar(2, -1);//初始化大小2并将初始值置为-1
		map<int, int> hashTable;
		for (int i = 0; i < nums.size(); ++i)
		{
			if (hashTable.count(targe - nums[i])) //.count返回当前值出现的次数
			{
				retTar[0] = hashTable[targe - nums[i]];
				retTar[1] = i;
				return retTar;

			}
			hashTable[nums[i]] = i;
		}

		return{};
	}
};

/*
	1. 排除大于targe的值. -> ×, 存在未负数的情况, 当为负数的时候允许大于9
	2. 利用 targe - nums[i] = nums[j];属于暴力搜索 时间复杂度是 n * (n- 1);
	3. 采用map来做处理
*/
int main()
{
	vector<int> nums = { 2, 7, 11, 15 };
	int targe = 13;
	Solution m;

	vector<int> temp = m.twoSum(nums, targe);

	for (auto i : temp)
	{
		cout << i << endl;
	}

	return 0;
}
```

