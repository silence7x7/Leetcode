# Leetcode
# 算法类
## 二分查找

# 数据结构
what is strcat,strcat的第一第二参数不能是char 'a','c'必须是char* 或者是char[]???

FizzBuzz
```c++
class Solution {
public:
    vector<string> fizzBuzz(int n) {
        vector<string> res;
        for(int i=1;i<=n;++i){
            if((i%3==0)&&(i%5!=0))res.push_back("Fizz");
            else if((i%3!=0)&&(i%5==0))res.push_back("Buzz");
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
