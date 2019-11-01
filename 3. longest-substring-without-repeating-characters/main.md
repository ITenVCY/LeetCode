```c++
/*
Given a string, find the length of the longest substring without repeating characters.

Example 1:

Input: "abcabcbb"
Output: 3
Explanation: The answer is "abc", with the length of 3.
Example 2:

Input: "bbbbb"
Output: 1
Explanation: The answer is "b", with the length of 1.
Example 3:

Input: "pwwkew"
Output: 3
Explanation: The answer is "wke", with the length of 3.
Note that the answer must be a substring, "pwke" is a subsequence and not a substring.
*/

#include <iostream>
#include <map>
#include <string>

using namespace std;

class Solution {
public:
	int lengthOfLongestSubstring(string s) {
		map<char, int> mp;
		int max = 0;

		for (int i = 0; i < s.size(); ++i)
		{
			if (mp.find(s[i]) == mp.end())
			{
				mp[s[i]] = i;
				if (max < mp.size())
				{
					max = mp.size();
				}
			}
			else
			{
				i = mp[s[i]];
				mp.clear();

			}

		}

		return max;
	}
};


int lengthOfLongestSubstring(char * s) {
	int start = 0, end = 0, maxlen = 0;
	char map[256] = { 0 };
	map[(int)*(s + start)] = 1;

	while (*(s + end) != 0)
	{
		maxlen = maxlen > (end - start + 1) ? maxlen : (end - start + 1);
		++end;
		while (0 != map[(int)*(s + end)])//将要加入的新元素与map内元素冲突
		{
			map[(int)*(s + start)] = 0;
			++start;
		}
		map[(int)*(s + end)] = 1;
	}

	return maxlen;
}

int main()
{
	string s = "dvdf";
	Solution sl;
	
	int ret = sl.lengthOfLongestSubstring(s);
	ret = lengthOfLongestSubstring("abcbcanmk");
	return 0;
}
```

