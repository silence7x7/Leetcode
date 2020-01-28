- [为什么c++不提供split--知乎](https://www.zhihu.com/question/36642771)


最优雅的split写法：
```c++
static void split(const string& s, vector<string>& tokens, const string& delimiters = " ")
{
        string::size_type lastPos = s.find_first_not_of(delimiters, 0);
        string::size_type pos = s.find_first_of(delimiters, lastPos);
        while (string::npos != pos || string::npos != lastPos) {
                tokens.push_back(s.substr(lastPos, pos - lastPos));
                lastPos = s.find_first_not_of(delimiters, pos);
                pos = s.find_first_of(delimiters, lastPos);
        }
}
```
附带了一个emplace_back和push_back问题，前者速度快一倍

- [参考文章](https://stackoverflow.com/questions/26328793/how-to-split-string-with-delimiter-using-c)

附上多个string函数
```c++
#include <iostream>
#include <string>
#include <vector>
#include <map>

using namespace std;
//剔除函数
static string& strip(string& s, const string& chars = " ")
{
        s.erase(0, s.find_first_not_of(chars.c_str()));//删除前面的空格
        s.erase(s.find_last_not_of(chars.c_str()) + 1);//删除后面空格
        return s;
}
//分割函数
static void split(const string& s, vector<string>& tokens, const string& delimiters = " ")
{
        string::size_type lastPos = s.find_first_not_of(delimiters, 0);
        string::size_type pos = s.find_first_of(delimiters, lastPos);
        while (string::npos != pos || string::npos != lastPos) {
                tokens.push_back(s.substr(lastPos, pos - lastPos));
                lastPos = s.find_first_not_of(delimiters, pos);
                pos = s.find_first_of(delimiters, lastPos);
        }
}

static void parse(string& s, map<string,string>& items)
{
        vector<string> elements;
        s.erase(0, s.find_first_not_of(" {"));
        s.erase(s.find_last_not_of("} ") + 1);
        split(s, elements, ",");
        for (vector<string>::iterator iter=elements.begin(); iter != elements.end(); iter++) {
                vector<string> kv;
                split(*iter, kv, ":");
                if (kv.size() != 2) continue;
                items[strip(kv[0], " \"")] = strip(kv[1], " \"");
        }
}

int
main()
{
        string data = "  {  \"key1\"  :  \"data1\"  ,  \"key2\"  :  \"data2\"    }  ";
        map<string,string> items;
        parse(data, items);

        for (map<string,string>::iterator iter=items.begin(); iter != items.end(); iter++) {
                cout << "key=" << (*iter).first << ",value=" << (*iter).second << endl;
        }
}
```
