# -151-201506020414-
cc
#include<bits/stdc++.h>#include<string.h>
using namespace std;void cal_next(char *source, int *next, int len){    next[0] = -1;                              //next[0]初始化为-1，-1表示不存在相同的最大前缀和最大后缀    int k = -1;                                //k初始化为-1    for (int q = 1; q <= len-1; q++)    {        while (k > -1 && source[k + 1] != source[q])//如果下一个不同，那么k就变成next[k]，注意next[k]是小于k的，无论k取任何值。        {            k = next[k];                           //往前回溯        }        if (source[k + 1] == source[q])//如果相同，k++        {            k = k + 1;        }        next[q] = k;//这个是把算的k的值（就是相同的最大前缀和最大后缀长）赋给next[q]    }}int KMP(char *source, int slen, char *target, int plen){    int *next = new int[plen];    cal_next(target, next, plen);                //计算next数组    int k = -1;    for (int i = 0; i < slen; i++)    {        while (k >-1&& target[k + 1] != source[i])//target和source不匹配，且k>-1（表示target和source有部分匹配）            k = next[k];                          //往前回溯        if (target[k + 1] == source[i])            k = k + 1;        if (k == plen-1)                          //说明k移动到target的最末端        {                                                   return i-plen+1;                      //返回相应的位置        }    }    return -1;  }int main(){ char *source ="bhsnsdgfjgkshkhfbabachjhfkye";    char *target ="babac";    int i=strlen(source);    int j=strlen(target);    int a = KMP(source,i, target,j);    cout<<"在原字符串的第"<<a<<"个位置有匹配的字符串"<<endl;    return 0;}






