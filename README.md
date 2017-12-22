# infa
// row2.cpp: определяет точку входа для консольного приложения.
//

#include "stdafx.h"
#include<iostream>
#include <cmath>
#include <algorithm>
using namespace std;

double f(int n, double x) {
	double retValue = x;
	double prevValue=x;
	for (int i = 2; i <= n; i++) {
		prevValue *= x*(i - 1) / i;
		retValue += prevValue;
	}
	retValue *= -1;
	return retValue;
}

int main()
{
	const double EXACT = 0.00001;
	int s = 0;
	for (double x = 0.1; x <= 0.9; x += 0.08) {
		double prprev = -x;
		double prevValue = x * x / 2;
		double prev = prprev - prevValue;
		int counter = 2;
		while (abs(prev - prprev) > EXACT) {
			counter++;
			prevValue *= x*(counter - 1) / counter;
			prprev = prev;
			prev = prprev - prevValue;
		}
		s = max(s, counter);
	}
	cout << s << endl<<endl;
	for (double x = 0.1; x <= 0.9; x += 0.08) {
		cout << "log=" << log(1 - x) << " f=" << f(s, x) << endl;
	}

    return 0;
}
