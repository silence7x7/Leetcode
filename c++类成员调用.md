```c++
class tt1{
public:
	void pf(int x){
		cout<<x<<"\n";
	}
};
int main(){
	//调用类的函数：
	//方式1：
	tt1().pf(3);
	//方式2：
	tt1 ttt;
	ttt.pf(5);
	return 0;
}
```
