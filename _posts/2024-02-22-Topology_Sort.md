---
title: "Topology Sort:위상정렬"
author: 임희수
date: 2024-02-22 00:30:00 +0900
categories: [Development, Algorithm]
tags: [Topology Sort]
---
## **BFS(너비우선탐색)란?**
<img src = "/assets/img/Topology_sort_picture/Topology_sort.gif" alt="picture" width="300" height="300">
- **위상정렬**은 **순서가 정해져 있는 그래프**를 탐색할 때 사용할 수 있는 방법이다.
- 노드로 들어가는 간선의 개수, 즉 **진입차수**를 이용하여 그래프의 순서를 결정해준다.
- 위상정렬은 **진입차수가 0**인 노드들을 방문하고 이와 **연결되어있는 간선들을 제거**(진입차수를 낮춤)하는 것을 반복하며 진행된다.
- 하지만 사이클이 발생하는 경우 사이클이 발생하는 곳부터 진입차수가 0이 되는 노드가 없어지게 되므로 탐색을 멈추게 된다. 그렇기 때문에 **DAG: Directed Acyclic Graph(유향 비순환 그래프)**에서만 정의될 수 있다.
- 분리되어 있는 그래프에서도 사용이 가능하며, 조건에 따라 정답이 다양하게 나올 수 있다. 예시를 들어 위 GIF를 보면 **1->2->3->4->5->7->6->8** 순으로 탐색을 하는데 따로 조건이 있지 않다면 2와 3의 탐색 순서가 바뀐 **1->3->2->4->5->6->7->8**도 정답이 될 수 있다.

<br>
## **작동과정**
<br>
<table width="50%" align="center">
  <tr>
    <td rowspan= "3" width="50%"><img src = "https://HuisuLim.github.io/assets/img/Topology_sort_picture/그림1.png" alt="picture"></td>
    <td><img src = "https://HuisuLim.github.io/assets/img/Topology_sort_picture/표1.png" alt="picture"></td>
  </tr>
  <tr>
    <td><figure>
      <figcaption>Queue</figcaption>
      <img src = "https://HuisuLim.github.io/assets/img/Topology_sort_picture/큐1.png" alt="picture">
    </figure></td>
  </tr>
  <tr>
    <td><figure>
      <figcaption>Result</figcaption>
      <img src = "https://HuisuLim.github.io/assets/img/Topology_sort_picture/결과1.png" alt="picture">
    </figure></td>
  </tr>
</table>
- 위와 같은 그래프에서 위상정렬을 진행한다고 하자. 출력된 노드는 초록색으로 색칠하겠다.

<br>
<table width="50%" align="center">
  <tr>
    <td rowspan= "2" width="50%"><img src = "https://HuisuLim.github.io/assets/img/Topology_sort_picture/그림2.png" alt="picture"></td>
    <td><img src = "https://HuisuLim.github.io/assets/img/Topology_sort_picture/표2.png" alt="picture"></td>
  </tr>
  <tr>
    <td><figure>
      <figcaption>Queue</figcaption>
      <img src = "https://HuisuLim.github.io/assets/img/Topology_sort_picture/큐2.png" alt="picture">
    </figure></td>
  </tr>
</table>
- 처음에 방문해야 할 진입차수가 0인 노드들을 탐색해보면, 1번 노드 밖에 존재하지 않는다. 1번 노드를 큐에 삽입한다.

<br>
<table width="50%" align="center">
  <tr>
    <td rowspan= "2" width="50%"><img src = "https://HuisuLim.github.io/assets/img/Topology_sort_picture/그림3.png" alt="picture"></td>
    <td><img src = "https://HuisuLim.github.io/assets/img/Topology_sort_picture/표3.png" alt="picture"></td>
  </tr>
  <tr>
    <td><figure>
      <figcaption>Queue</figcaption>
      <img src = "https://HuisuLim.github.io/assets/img/Topology_sort_picture/큐3.png" alt="picture">
    </figure></td>
  </tr>
</table>
- 큐의 front에 있는 노드는 1번 노드로 이를 출력 후 큐에서 pop한다.
- 1번 노드와 연결되어 있는 2번, 3번 노드의 간선을 제거해준다(진입차수를 1씩 낮춘다).
- 간선이 제거된(진입차수가 낮아진) 2번, 3번 노드는 진입차수가 0이 되었으므로 이들을 큐에 삽입한다.

<br>
<table width="50%" align="center">
  <tr>
    <td rowspan= "2" width="50%"><img src = "https://HuisuLim.github.io/assets/img/Topology_sort_picture/그림4.png" alt="picture"></td>
    <td><img src = "https://HuisuLim.github.io/assets/img/Topology_sort_picture/표4.png" alt="picture"></td>
  </tr>
  <tr>
    <td><figure>
      <figcaption>Queue</figcaption>
      <img src = "https://HuisuLim.github.io/assets/img/Topology_sort_picture/큐4.png" alt="picture">
    </figure></td>
  </tr>
</table>


<br>
<table width="50%" align="center">
  <tr>
    <td rowspan= "2" width="50%"><img src = "https://HuisuLim.github.io/assets/img/Topology_sort_picture/그림5.png" alt="picture"></td>
    <td><img src = "https://HuisuLim.github.io/assets/img/Topology_sort_picture/표5.png" alt="picture"></td>
  </tr>
  <tr>
    <td><figure>
      <figcaption>Queue</figcaption>
      <img src = "https://HuisuLim.github.io/assets/img/Topology_sort_picture/큐5.png" alt="picture">
    </figure></td>
  </tr>
</table>


<br>
<table width="50%" align="center">
  <tr>
    <td rowspan= "2" width="50%"><img src = "https://HuisuLim.github.io/assets/img/Topology_sort_picture/그림6.png" alt="picture"></td>
    <td><img src = "https://HuisuLim.github.io/assets/img/Topology_sort_picture/표6.png" alt="picture"></td>
  </tr>
  <tr>
    <td><figure>
      <figcaption>Queue</figcaption>
      <img src = "https://HuisuLim.github.io/assets/img/Topology_sort_picture/큐6.png" alt="picture">
    </figure></td>
  </tr>
</table>


<br>
<table width="50%" align="center">
  <tr>
    <td rowspan= "2" width="50%"><img src = "https://HuisuLim.github.io/assets/img/Topology_sort_picture/그림7.png" alt="picture"></td>
    <td><img src = "https://HuisuLim.github.io/assets/img/Topology_sort_picture/표7.png" alt="picture"></td>
  </tr>
  <tr>
    <td><figure>
      <figcaption>Queue</figcaption>
      <img src = "https://HuisuLim.github.io/assets/img/Topology_sort_picture/큐7.png" alt="picture">
    </figure></td>
  </tr>
</table>

<br>
<table width="50%" align="center">
  <tr>
    <td rowspan= "2" width="50%"><img src = "https://HuisuLim.github.io/assets/img/Topology_sort_picture/그림8.png" alt="picture"></td>
    <td><img src = "https://HuisuLim.github.io/assets/img/Topology_sort_picture/표8.png" alt="picture"></td>
  </tr>
  <tr>
    <td><figure>
      <figcaption>Queue</figcaption>
      <img src = "https://HuisuLim.github.io/assets/img/Topology_sort_picture/큐8.png" alt="picture">
    </figure></td>
  </tr>
</table>

<br>
<table width="50%" align="center">
  <tr>
    <td rowspan= "2" width="50%"><img src = "https://HuisuLim.github.io/assets/img/Topology_sort_picture/그림9.png" alt="picture"></td>
    <td><img src = "https://HuisuLim.github.io/assets/img/Topology_sort_picture/표8.png" alt="picture"></td>
  </tr>
  <tr>
    <td><figure>
      <figcaption>Queue</figcaption>
      <img src = "https://HuisuLim.github.io/assets/img/Topology_sort_picture/큐9.png" alt="picture">
    </figure></td>
  </tr>
</table>

<br>
<table width="50%" align="center">
  <tr>
    <td rowspan= "2" width="50%"><img src = "https://HuisuLim.github.io/assets/img/Topology_sort_picture/그림10.png" alt="picture"></td>
    <td><img src = "https://HuisuLim.github.io/assets/img/Topology_sort_picture/표8.png" alt="picture"></td>
  </tr>
  <tr>
    <td><figure>
      <figcaption>Queue</figcaption>
      <img src = "https://HuisuLim.github.io/assets/img/Topology_sort_picture/큐9.png" alt="picture">
    </figure></td>
  </tr>
</table>

<br>
<table width="50%" align="center">
  <tr>
    <td rowspan= "2" width="50%"><img src = "https://HuisuLim.github.io/assets/img/Topology_sort_picture/그림7.png" alt="picture"></td>
    <td><img src = "https://HuisuLim.github.io/assets/img/Topology_sort_picture/표7.png" alt="picture"></td>
  </tr>
  <tr>
    <td><figure>
      <figcaption>Queue</figcaption>
      <img src = "https://HuisuLim.github.io/assets/img/Topology_sort_picture/큐7.png" alt="picture">
    </figure></td>
  </tr>
</table>


<br>
## **C++ 구현**

```cpp
#include <iostream>
#include <vector>
#include <queue>
using namespace std;

vector<int> graph[9];
int inDegree[9];

void topology_sort(){
    queue<int> q;
    for(int i = 1; i<=8; i++){
        if(inDegree[i] == 0){
            q.push(i);
        }
    }

    for(int i = 1; i<=8; i++){

        if(q.empty()){
            cout << "사이클 발생" << endl;
        }

        int node = q.front();
        cout << node << " ";
        q.pop();
        for(int j = 0; j < graph[node].size(); j++){
            int nextNode = graph[node][j];
            inDegree[nextNode]--;
            if(inDegree[nextNode] == 0){
                q.push(nextNode);
            }
        }
    }
}

int main(){
    
    graph[1].push_back(2);
    graph[1].push_back(3);
    inDegree[2]++;
    inDegree[3]++;

    graph[2].push_back(4);
    inDegree[4]++;

    graph[3].push_back(4);
    graph[3].push_back(5);
    inDegree[4]++;
    inDegree[5]++;

    graph[4].push_back(6);
    inDegree[6]++;

    graph[5].push_back(6);
    graph[5].push_back(7);
    inDegree[6]++;
    inDegree[7]++;

    graph[7].push_back(6);
    graph[7].push_back(8);
    inDegree[6]++;
    inDegree[8]++;

    topology_sort();

}
```

<br>
## **시간복잡도**
- V(Vertex) = 정점, E(Edge) = 간선
  위상정렬은 V번 실행되어야 한다. 그 전에 실행이 끝나면 사이클이 발생한 것이다.
  그리고 최종적으로 모든 간선을 확인하므로 시간복잡도는 **O(V+E)**가 된다.
