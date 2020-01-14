# Leetcode
# 算法类
## 二分查找

# 数据结构
what is strcat,strcat的第一第二参数不能是char 'a','c'必须是char* 或者是char[]???

- 412(Easy)[FizzBuzz](https://leetcode-cn.com/problems/fizz-buzz/)
```c++
class Solution {
public:
    vector<string> fizzBuzz(int n) {
        vector<string> res;
        for(int i=1;i<=n;++i){
            if((i%3==0)&&(i%5!=0))res.push_back("Fizz");
            else if((i%3!=0)&&(i%5==0))res.push_back("Buzz");//其实不用这么复杂判断，看下面版本精简if判断
            else if((i%3==0)&&(i%5==0))res.push_back("FizzBuzz");
            //else res.push_back(i);int给string是错误的
            //十进制转为string，方法一
            else{
                string s;
                int j=0;
                while(i!=0){
                    s[j++]=i%10+'0';
                    i/=10;
                }
                reverse(s.begin(),s.end());
                res.push_back(s);
                
            }
            //十进制转为string，方法二
            //    for(; n/10 != 0; n /= 10)
            //    s[i++] = n%10 + '0';
            
            
        }
        return res;
    }
};
```
上面这代码显示内存超了，初想是不是定义了vector，然后使用太多push_back导致。

加了res.resize(n);把所有push_back换为res[i]="xxx";但时间超了

if注意先判断%15，不然上面版本的代码if判断冗杂

进阶：不需要判断15的整除，能被15整除的数让它既走整除3的逻辑也走5的逻辑就可以了，需要一点小技巧。
```c++
    //这么做击败99%
    vector<string> fizzBuzz(int n) {
        vector<string> res;
        for(int i = 1;i <= n;++i){
            if(i%15 == 0) res.push_back("FizzBuzz");
              else if(i%3 == 0) res.push_back("Fizz");
                  else if(i%5 == 0) res.push_back("Buzz");
                      else res.push_back(to_string(i));
        }
        return res;
    }
```
to_string()
