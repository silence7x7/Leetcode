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
<summary>大数阶乘</summary>
      
```c++

```
</details>
