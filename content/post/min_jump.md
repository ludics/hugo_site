---
title: "Min Jump"
date: 2019-04-13T01:04:00+08:00
tags: ['Algorithm', 'Code']
draft: false
---

## 页面最小跳转次数
电商网站中，web页面之间可以互相跳转。给定用户路径中的起始页面和终点页面，计算用户路径中，这两个页面间最少需要经过的跳转次数。

请使用标准输入输出(stdin，stdout)；请把所有程序写在一个文件里，勿使用已禁用图形、文件、网络、系统相关的头文件和操作，如sys/stat.h , unistd.h , curl/curl.h , process.h

时间限制: 1S (C/C++以外的语言为: 3 S)   

内存限制: 64M (C/C++以外的语言为: 576 M)

输入:

第一行包含两列，为起始页面和终止页面的名称。
第二行到最后一行为用户行为日志，其中第一列为当前页面名称，第二列为上一页面名称。第二行的NULL表示第一个页面的上级页面为空。每列数据之间以逗号','为分隔符，具体请见输入范例。

输出:

上述用户的行为路径中，页面A到页面F有以下两种方式 

1. A->B->D->E->F
2. A->E->F

此时方式2跳转次数最少，为2

输入范例:
```
A,F
A,NULL
B,A
D,B
F,B
E,A
F,E
E,D
D,B
C,B
B,G
G,F
C,F
```

输出范例:

```
2
```

### Python解法

{{< highlight python "nowrap=false">}}
l=[["A","F"], ["A","NULL"], ["B","A"], ["D","B"], ["F","B"], ["E","A"],
   ["F","E"], ["E","D"], ["D","B"], ["C","B"], ["B","G"], ["G","F"], ["C","F"]]
start=l[0][0]
target=l[0][1]
l=l[1:]
l1=[]
def f(start,target,m=0):
    for i in range(len(l)):
        if l[i][1]==start and l[i][0]==target:
            return m+1
        if l[i][1]==start and l[i][0]!=target:
            l1.append(f(l[i][0],target,m+1))
    return min(l1)
print(f(start,target))
{{</ highlight >}}

### C++解法

[Gist Code: min_jump.cpp](https://gist.github.com/ludics/6ad5459b6e2ddfbd9381be02949f754d)

{{< highlight C "nowrap=false">}}
#include<iostream>
#include<vector>
#include<string>
#include<algorithm>
#include<stack>

using namespace std;

int get_index(vector<string>& vs, string str){
    vector<string>::iterator it = find(vs.begin(), vs.end(), str);
    if(it == vs.end()){
        vs.push_back(str);
        return vs.end() - vs.begin() - 1;
    }
    else return it - vs.begin();
}

struct Node{
    string data;
    int id;
    struct Node* next;
    Node(string d, int i, struct Node *n=NULL) {
        data = d;
        id = i;
        next = n;
    } 
};

typedef pair<Node*, int> node_l;

int dfs(vector<Node*> graph, int start_id, int end_id){
    vector<int> vlen;
    stack<pair<Node*, int> > sn; 
    Node* ps = graph[start_id];
    pair<Node*, int> tmp(ps, 0);
    sn.push(tmp);
    while(!sn.empty()){
        pair<Node*, int> nl = sn.top();
        sn.pop();
        Node* p = nl.first;
        int level = nl.second;
        if(p->id == end_id){
            vlen.push_back(level);
            continue;
        }
        else{
            p = p->next;
            while(p){
                tmp = make_pair(graph[p->id], level + 1);
                sn.push(tmp);
                p = p->next;
            }
        }
    }
    return *min(vlen.begin(), vlen.end());
}

int main(){
    ios::sync_with_stdio(false);
    vector<string> vs;
    string start, end;
    getline(cin, start, ',');
    getline(cin, end);
    string from, to;
    vector<Node*> graph;
    // 建图，邻接表法表示
    while(!cin.eof()){
        getline(cin, to, ',');
        if(to=="") break;
        int id_to = get_index(vs, to);
        if(id_to >= graph.size()){
            Node *nn = new Node(to, id_to);
            graph.push_back(nn);
        }
        getline(cin, from);
        int id_fr = get_index(vs, from);
        if(id_fr >= graph.size()){
            Node *nn_f = new Node(from, id_fr);
            graph.push_back(nn_f);
        }
        Node *p, *q;
        bool flag = true;
        for(p = graph[id_fr]; p != NULL; p = p->next){
            q = p;
            if(q->data == to) flag = false;
        }
        if(flag){
            Node *nn = new Node(to, id_to);
            nn->next = NULL;
            q->next = nn;
        }
    }
    int start_id = get_index(vs, start);
    int end_id = get_index(vs, end);
    cout << dfs(graph, start_id, end_id) << endl;
    return 0;
}
{{</ highlight >}}

