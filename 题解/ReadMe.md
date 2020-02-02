- [手写split](https://github.com/silence7x7/Leetcode/blob/master/%E9%A2%98%E8%A7%A3/split.md)
- [手写indexOf](https://www.cnblogs.com/zhangshi/p/6502987.html)
- [练习题](https://leetcode-cn.com/problems/word-pattern/)

      两种方法，map+set  /  indexOf
<details>
<summary>大数阶乘</summary>

```c++
//用long数组存储阶乘结果，数组中的每个数存储阶乘的4位10进制数，不足的用0补充。
#include <stdio.h>
long res[10000];
int factorial(const int n){
    int i,j,carry,bit;
    for(res[bit=carry=0]=i=1;i<=n;++i,carry=0){
        for(j=0;j<=bit;++j){
            res[j]=res[j]*i+carry;
            carry=res[j]/10000;
            res[j]%=10000;
        }
        if (carry) res[++bit]=carry;//如果进位就要高位再开一位写数字
    }
    for(printf("%ld",res[i=bit]);i;printf("%4.4ld",res[--i]));
    //%04d代表4位数，高位补0。但大佬都用%4.4ld为什么？
    return printf("\n");
}
int main(){
    for(int n;~scanf("%d",&n);factorial(n));
    //~是按位取反。scanf的返回值是输入值的个数
    //如果没有输入值则返回-1。对于-1按位求反得到0。所以如果没有输入则退出循环
    //常用while(~scanf())代替while(sacnf()!EOF)和while(sacnf()==2).
    //因为EOF定义为-1，所以用这个代替
    //但有漏洞：输入字母会陷入死循环
    //一旦输入的值为字符等不能成功赋值的量，scanf()赋值不成功，会把读到的内容又返回到stdin缓冲区，
    //且取反值使得while又进入到下一次循环，scanf()又从stdin缓冲区读到相同的内容，这样就形成了死循环……
    return 0;
}
```
</details>


<details>
<summary>printf各种输出</summary>
      
```c++
printf("%4d,",a[i]);
 123,   4,   3,   2,   1,   0,
//输出4位，用空格补

printf("%04d",a[i]);
0123,0004,0003,0002,0001,0000,
//用0补，但是不能用%14d,这不是用1补，而是14位空格补
同上
printf("%.4d",a[i]);
0123,0004,0003,0002,0001,0000,

printf("%4.3d",a[i]);
 123, 004, 003, 002, 001, 000,
//输出4位，0补3位
printf("%4.4d",a[i]);
0123,0004,0003,0002,0001,0000,
//输出4位，0补4位
```
</details>


<details>
<summary>欧几里得算法最大公约数</summary>
      
```c++
int gcd(int a, int b)//欧几里得算法求最大公约数
{
    if(b==0) return a;
    else return gcd(b, a%b);
}

//判断
gcd(buf[i], buf[j])==1代表最大公约数为1，即不能化简约分
算法精妙在于会自动交换a，b，太秀了
```
</details>

<details>
<summary>迭代器失效</summary>

```c++
//在vector迭代器遍历时删除或插入数据，导致迭代器失效
vector<int> ans(4);
    ans[0]=1;
    for(auto n:ans)
    	if(n!=0)ans.push_back(9);
    int i=0;
    for(auto n:ans){
        cout<<i<<"  "<<n<<endl;
	  i++;
    }
 //得到输出结果：
0  1
1  0
2  0
3  0
4  9
5  9
并不会一直增长，因为vector动态增长原理，遍历时vec就这么大，迭代器遍历时不会改变大小。
所以最后并不会无限插入数据9
```
reference:  
[可以vec改用list解决](https://blog.csdn.net/hechao3225/article/details/55101344)  
[迭代器失效](https://blog.csdn.net/petersmart123/article/details/53304437)
</details>

<details>
<summary>string compare函数</summary>
      
- [compare](http://www.cplusplus.com/reference/string/string/compare/)  
```c++
str1.compare(0,i,str2,0,i)==0//str1的0开始i个长度与str2的0开始i个长度比较。
```
c语言<string.h>用的是[strcmp](https://www.runoob.com/cprogramming/c-function-strcmp.html)

</details>

<kbd>string</kbd>+<kbd>tree</kbd>+<kbd>DP</kbd> 

<details>
<summary>printf和cout混合使用出问题</summary>

```c++
printf("A\n");
cout<<"B\n";
printf("C\n");

the out put is:
A
C
B
not:
A
B
C
explanation:
1.   you   shouldn't   mix   "printf()"   and   "cout"   in   the   same   program   
because   C   stdio   and   C++   iostreams   are   completely   independent   
and   they   may   have   different   buffering   scheme   and   they   don't   share   the   same   buffer,  
so   the   ouput   may   come   out   in   an   order   that   you   are   not   expecting,   
that   is   probably   what   happened   in   your   case  .
   
2.   try  
   
  cout   <<   "B"   <<   endl;  
   
  or   call    
   
  ios::sync_with_stdio();

```
</details>

<details>
<summary>ssssssss</summary>

```c++


```
</details>

