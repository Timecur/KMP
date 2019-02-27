# KMP

#include <iostream>
#include <stdlib.h>
#include <vector>
#include <string>

using namespace std;

// i为后缀，j为前缀
void GetNext(string T, vector<int> next)
{
	int i = 1;
	int j = 0;
	next[1] = 0;

	// 前缀是固定的，后继是相对的
	while (i < T.size()){
		if (0 == j || T[i] == T[j]){
			i++;
			j++;
			if (T[i] != T[j]){
				next[i] = j;
			}
			else
			{
				next[i] = next[j];
			}
		}
		else
		{
			j = next[j];
		}
	}
}

// 返回子串T 在主串S 第pos个字符之后的位置
// 若不存在返回0
int IndexKMP(string S, string T, int pos)
{
	int i = pos;
	int j = 1;
	vector<int> next(255);

	GetNext(T, next);

	while (i <= S[0] && j <= T[0]){
		if (0 == j || S[i] == T[j]){
			i++;
			j++;
		}
		else{
			j = next[j];
		}
	}

	if (j > T[0]){
		return i - T[0];
	}
	else{
		return 0;
	}
}
