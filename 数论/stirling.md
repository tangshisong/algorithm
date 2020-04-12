stirling公式：<img src="https://latex.codecogs.com/png.latex?n!\approx&space;\sqrt{2&space;\pi&space;n}&space;(\frac{n}{e})^{n}" title="n!\approx \sqrt{2 \pi n} (\frac{n}{e})^{n}" align="middle" />

# 估计阶乘的位数

<img src="https://latex.codecogs.com/png.latex?lg(n!)=&space;\left&space;\lfloor&space;\frac{lg(2\pi&space;n)}{2}&space;&plus;&space;nlg\frac{n}{e}\right&space;\rfloor&space;&plus;&space;1" title="lg(n!)= \left \lfloor \frac{lg(2\pi n)}{2} + nlg\frac{n}{e}\right \rfloor + 1" />

```cpp
#include<bits/stdc++.h>
using namespace std;
const double e=exp(1.0);
const double PI=acos(-1.0);
int main()
{
	int T,n;
	double ans;
	scanf("%d",&T);
	while(T--)
	{
		scanf("%d",&n);
		ans=log10(sqrt(2.0*PI*n))+(double)n*log10((double)n/e);
		printf("%d\n",(int)ceil(ans));
	}
	return 0;
}
```
