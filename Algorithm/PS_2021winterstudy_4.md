# 4.

## DFS/BFS 개요

일반적으로 문제 해결 차원에서 중요하고, 코딩테스트에서 자주 등장하는 유형이다. 미리 기본적인 그리기, 브루트포스 풀어보지 않았다면 DFS/BFS. 빠르고 쉽게 구현하는 언어가 c++.

dfs/bfs 기본개념 선행지식 알아보기

* 대표적인 탐색 알고리즘 : 최단 경로, 최소 비용 ... 탐색 기준에 맞춰서 원하는 데이터를 찾는 과정이다. 
    * 탐색이란 많은 데이터 중에서 원하는 데이터를 찾는 과정
    * 대표적인 그래프 탐색 알고리즘은 DFS와 BFS
    * DFS/BFS는 코딩테스트에서 매우 자주 등장하는 유형
    * node,vector,edge로 이루어짐 / 사이클이 생기는 부분은 벨만 포워드 / 거의 안쓰이지만, 기억해두는 과정에서 weigt 명칭을 쓰기도 함. 여러 기준이 있을 수 있다.
    * 실제 문제에서는 그래프 input, 개체 그 자체가 아니라 데이터로 들어옴


* 그래프를 구성하는 방법 두 가지
    * 이차원 배열
    * 연결 리스트
* 이차원 배열을 사용하면 공간 많이 차지, 간단 (이진수 혹은 weigt)
* 연결 리스트는 공간은 적게 차지하지만 복잡 (직관적 파악, overhead, 메모리 낭비)
* **2차원배열이 많이 쓰이지만, 링크드 리스트 방법에 대한 설명과 구현도 면접에서 필요할 수 있다. 링크드 리스트가 heap(x)(배열로 구현) stack(o) 스택을 구현하는 방법 2가지**


* 먼저 알아야하는 자료구조 및 기법
    * 스택
        * 스택이 어떤 서비스에서 많이 쓰이나? 인터넷 어플.
        * DFS 사용할 때, 스택 쓸 때는, dfs(깊이 기반). 갔던 경로를 기억해놔야 경로를 기억하는데 스택 자료구조를 사용할 수 있음. 
    * 큐
        * 큐는 bfs. 너비 우선 탐색해서 큐에는 enqueue, 앞으로 봐야할 친구들을 넣는 구조. 앞으로 가야할 길들을 저장해놓고, 들어가는 순서, 나오는 순서.
    * 재귀함수
        * 스택이랑 같은 개념. bfs를 구현해야하면 큐를 사용해야한다. dfs를 구현해야한다. 스택or재귀함수. 재귀함수에 대한 부분도 알아야한다. 스택을 사용할 때, 이전에 갔던 경로들을 기억하기 위한 자료구조라고 했는데, 재귀함수도 마찬가지로 팩토리알을 예로 들 때 팩토리알. 경로를 기억했다가 나가는 경로를 찾아가는 용도.

## dfs? 이미 알고 있다
*  Fibonacci
피보나치 수열, 재귀로 구현. 트리 형태로 그래프를 그려서 만들어지는 형태. 이것도 dfs. 피보나치 설명. 면접 단골 질문: 피보나치. 재귀식으로 피보나치 구현? 피보나치 구현 3가지. 피보 재귀식 구현하면 중복된 경로가 많이 생겨서, 중복된 것을 반환하면서 사용하기 어려움. 이런 경로에서 메모리제이션, 이터레이션, .. 찾아보기
* n-queen
백트래킹 설명하면서 dfs 기반이라고 했음. 

## dfs와 bfs 기본
dfs와 bfs 어떤 것인가? 그래프 탐색의 목적은 모든 정점을 한 번씩 방문하는 것.
어떻게 방문할 것이냐에 따라 dfs와 bfs로 나뉨

* DFS 
    * 깊이 우선 탐색
    * DFS의 기본 작동 방식은 stack을 이용해서 갈 수 있는만큼 최대한 깊이 가고, 더 이상 갈 곳이 없다면 이전 정점으로 되돌아가는 것
    * stack과 recursive function을 이용하여 구현
* BFS
    * 너비 우선 탐색. 같은 레벨.
    * BFS의 기본 작동 방식은 queue를 이용하여 지금 위치에서 갈 수 있는 것들을 모두 큐에 넣는 방식
    * BFS는 queue와 while loop을 이용하여 구현
    * queue에 아무 노드가 남아있지 않으면 탐색은 끝났다고 가정하고 while loop에서 벗어남

- 예제: 백준 15552번 최대 힙 / 삼성 기출 문제
```cpp
#include <iostream>
#include <queue>
#include <cstring> //memset

using namespace std;

const int MAX = 1000 + 1;

int N,M,V;
int graph[MAX][MAX];
bool visited_vertices[MAX];

void DFS(int cur_vertex)
{
    cout << cur_vertex << " ";

    for(int i=1; i<=N; i++){
        if(graph[cur_vertex[i] && !visited_vertices[i]){
            visited+_vertices[i] = true;
            DFS(i);
        }
    }
}

void BFS(int cur_vertex)
{
    queue<int> queue;

    queue.push(cur_vertex);
    visited_vertices[cur_vertex] = true;

    while(!queue.empty()){
        cur_vertex = queue.front();
        queue.pop();

        cout << cur_vertex << " " ;
        
        for(int i=1; i<=N; i++){
            if(graph[cur_vertex][i] && !visited_vertices[i]){
                visited_vertices[i] = true;
                queue.push(i);
            }
        }
    }
}

int main(void)
{
    ios_base::sync_with_stdio(0);
    cin.tie(0);
    cin >> N >> M >> V;

    for(int i=0; i<M ; i++)
    {
        int start_node, end_node;
        cin >> start_node >> end_node;
        graph[start_node][end_node] = 1;
        graph[end_node][start_node] = 1;
    }

    visited_vertices[V] = 1;
    DFS(V);
    cout << "\n";

    memset(visited_vertices, false, sizeof(visited_vertices));
    BFS(V);
    cout << "\n";

    return 0;
}
```
## 1260번 dfs와 bfs.
두 문제는 꼭 풀기. 과제에 삼성 기출 문제.
dfs와 bfs 어떤식으로 순회하는지에 대한 문제. bfs로 순회했을 때 어떤식으로? 

input 4 5 1
4를 잇는 선의 개수 5개

주어지는 방향은 양방향이다. 
어떤 순서로 순회? 

dfs: 깊이 우선. 1->2 2->4 4->3 = 1243
bfs: 1 2 3 4

예제: 들어오게 되는 순서.
dfs: 34521
bfs: 34152
사실 노드 순서는 크게 중요하지 않음. 이런식으로 나오지 않음
먼저 연결된 순서를 보면 된다.
들릴 때마다 1 체크. 
dfs 코드는 간단하다. 현재의 vertex 출력해주고, 갈 수 있는 경로를 출력하고, 반복문으로 해준다. 이차원 배열, 배열의 row만큼 체크를 해줌. 그래프에 경로가 있는지, 이미 지나간 경로가 아닌지. 체크해주기. 그렇다고 하면 체크하고 dfs 이동
스택이 아니라 recursion으로 구현한 방식이다. 1260 c++
스택은 다음 예제 코드

memset, 지나간 경로 체크를 풀고 이후에 초기화해주는 명령
bfs를 돌리기. 큐라는 자료구조 사용.
다음에 갈 경로를 큐에 저장.
경로가 있어, 아ㄴ지나갔어, 다음에는 거기가자! (queue에 넣기)
whileloop에 큐가 없으면, 노드가 없으면

1) 그래프 만들기 2) 그래프 돌리기 3) 개행문자 출력
설명 연습 필요

## 2667: 단지번호 붙이기
실버1 평이
dfs/bfs : 실버 3~ 골드2 
난이도로 치면 중상

dfs/bfs 문제 중에서 그렇게 어려운 편에 속하는 문제는 아니다.
구역이 있다. 수원시에서 팔달구가 있고, 장안구 이런 게 있다. 집이 몇 채가 있는지.
기준은 연결되어있는지, 인접해있는지를 기준.
0이면 그 구역에 없다, 1이면 그 구역에 있다.

인접해있으니, 연결된 것 1단지+2단지+3단지

오름차순으로 정렬해서 출력해라.

for문을 돌 때 0인지 1인지. 1인 지역부터 dfs 시작. 1에서부터 갈 수 있는 경로 상하좌우

좌표
상 x,y+1
하 ...
direction 정의. 큰 손해가 없고 딜레이가 없어서 이런식으로 풀기도 함
경로 정하는 것부터 알아보면 x+y

int형 어레이를 선언하는 것과 같다. 하우스가 각 단지마다 몇개가 있는지를 넣어두는 vector. 각 단지마다 하우스가 몇 개가 있는지 기록. 
그래프를 만드는 과정이 나와 있다.
그래프 자체가 2차원 배열에 들어가게 된다. 체크가 안되어 있고, 

bfs로도 해보고, recursion, stackdfs

오름차순으로 하우스 정보를 출력하는 형태


리컬션 dfs. 방향4가지. 상하좌우
경로 구현. 스택. 다음 갈 경로. 
이전 경로를 기억하는 방식

bfs는 큐. 

3가지 방법중에 어떤것이 표준? 기능상으로 bfs dfs는 서로 풀 수 있음. 다만 메모리제한을 고려.
현재는 메모리가 작아 모두 성공.
recursion 멘토

recursion dfs가장 빠름. (외국자료)
깊은 단계에 대한 조건이 모호.
나오지 않는 테스트 케이스? 시간, 메모리.
메모리 기준으로 bfs가 더 쓸 것이다.(재귀식) 하지만 오히려 반대. 노드들만 기억하면되므로 저장공간의 수요가 비교적 적다.
목표 노드가 깊은 단계에 있을 경우 해를 빨리 구할 수 있다.

그래프 자체를 넘기는 경우가 있음.
메모리 손해, 시간적 오버헤드. 이런식으로 구현.행렬 시간복잡도는 같음. 누가 더 빠르다고 정의하기 


3가지 다 아님
결론: 문제에 따라 다르다.
일반적으로 : rec dfs! 테스트상 빠름. 일반적인 경우. 일반적이지 않은 경우. 뎁스가 끝이 없을 때, 재귀식 end 포인트 모호. => dfs

테스트 결과 설명 그래프를 임의로 만듦. n이 2520, 100이상 평균값. 최고depth는 24 depth,그래프 조건 같게 함. 조건을 같게 함. 스택이 recursion보다 느른 이유는 스택사용하면 pull을 많이 함. 재귀식으로 들어가는 단계에서 많지도 않음. 스택을 쓰면 pair자료가 있지만 오버헤드 큼 큐 마찬가지. 