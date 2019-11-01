```c++
#include <iostream>
#include <vector>

using namespace std;


/*
执行用时 :24 ms在所有 cpp 提交中击败了73.87%的用户
内存消耗 :10 MB, 在所有 cpp 提交中击败了79.90%的用户
*/
class Solution1{
public:
	double findMedianSortedArrays(vector<int>& nums1, vector<int>& nums2) {
		
		double rtn = 0.0;
		if (!nums1.size())
		{
			return nums2.size() % 2 ? nums2[nums2.size() / 2] : double(nums2[nums2.size() / 2 - 1] + nums2[nums2.size() / 2]) / 2.0;
		}
		if (!nums2.size())
		{
			return nums1.size() % 2 ? nums1[nums1.size() / 2] : double(nums1[nums1.size() / 2 - 1] + nums1[nums1.size() / 2]) / 2.0;
		}
		int flag = (nums1.size() + nums2.size()) % 2;
		int index = ((nums1.size() + nums2.size()) / 2) + 1;

		vector<int> tmp;

		size_t it1 = 0;
		size_t it2 = 0;

		while (1)
		{
			if (tmp.size() == index)
			{
				rtn = flag ? tmp[index-1] : double(tmp[index-1] + tmp[index -2]) / 2.0;
				break;
			}

			if (it1 >= nums1.size())
			{
				tmp.push_back(nums2[it2++]);
				continue;
			}
			if (it2 >= nums2.size())
			{
				tmp.push_back(nums1[it1++]);
				continue;
			}

			if (it2 == nums2.size() || nums1[it1] < nums2[it2])
			{
				tmp.push_back(nums1[it1++]);
			}
			else if (it1 == nums1.size() || nums1[it1] >= nums2[it2])
			{
				tmp.push_back(nums2[it2++]);
			}
		}
		return rtn;
	}
};

/*
执行用时 :20 ms, 在所有 cpp 提交中击败了88.72%的用户
内存消耗 :9.5 MB, 在所有 cpp 提交中击败了96.78%的用户
*/
class Solution2{
public:
	double findMedianSortedArrays(vector<int>& nums1, vector<int>& nums2) {

		double rtn = 0.0;
		if (!nums1.size())
		{
			return nums2.size() % 2 ? nums2[nums2.size() / 2] : double(nums2[nums2.size() / 2 - 1] + nums2[nums2.size() / 2]) / 2.0;
		}
		if (!nums2.size())
		{
			return nums1.size() % 2 ? nums1[nums1.size() / 2] : double(nums1[nums1.size() / 2 - 1] + nums1[nums1.size() / 2]) / 2.0;
		}
		int flag = (nums1.size() + nums2.size()) % 2;
		int index = ((nums1.size() + nums2.size()) / 2) + 1;

		size_t it1 = 0;
		size_t it2 = 0;
		int mid = 0;
		int midpre = 0;
		int count = 0;

		while (1)
		{
			if (count == index)
			{
				rtn = flag ? mid : double(midpre + mid) / 2.0;
				break;
			}

			count++;
			midpre = mid;

			if (it2 >= nums2.size())
			{
				mid = nums1[it1++];
				continue;
			}
			if (it1 >= nums1.size())
			{
				mid = nums2[it2++];
				continue;
			}

			if (nums1[it1] < nums2[it2])
			{
				mid = nums1[it1++];
				continue;
			}
		    if (nums1[it1] >= nums2[it2])
			{
				mid = nums2[it2++];
				continue;
			}
		}
		return rtn;
	}
};


int main()
{
	
	Solution2 s2;
	vector<int> nums1 = {-1}, nums2 = {3,4,7};

	double ret = s2.findMedianSortedArrays(nums1, nums2);

	return 0;
}
```

