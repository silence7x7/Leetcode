# 找错误

```c++
#include<iostream>
using namespace std;
int main(){
    int M;
    cin>>M;
    int N;
    cin>>N;
    int a[N];
    int i=0;
    while(N--){
        cin>>a[i++];
    }
    int cnt=0;
    i=N-1;
    while(M){
        if(M>=a[i]){
            cnt++;
            M-=a[i];
        }

        i--;
        //if(i<0&&M!=0)cout<<-1<<endl;//走到a[0] M还没减到0
        if(i<0)break;
    }
    if(M!=0)cout<<-1<<endl;
    else cout<<cnt<<endl;
}
```

因为N--了，导致i=N-1失效。
