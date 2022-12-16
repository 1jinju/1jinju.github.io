---
layout: post
title: Ch 14. 그래프
subtitle: 윤성우의 열혈 자료구조
cover-img: /assets/img/black.jpg
thumbnail-img: https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcEIsCe%2FbtrSRQqdi2q%2FegPvjWkpTIEh7d9mMaFlqk%2Fimg.png
share-img: /assets/img/path.jpg
tags: [자료구조]
---

# 14-1 그래프의 이해와 종류

## 그래프의 역사

- 쾨니히스베르크의 다리 문제
    
    모든 다리를 한 번씩만 건너서 처음 출발하는 장소로 돌아올 수 있는가
    
    ![Untitled](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fd0tyPa%2FbtrSJFjw4bR%2FWozcQW1PGR16uCnnOsvP4K%2Fimg.png)
    
    정점: 연결의 대상이 되는 개체 또는 위치  
    간선: 정점 사이의 연결  

<br>

## 그래프의 이해와 종류

- 무방향 그래프와 완전 그래프
    
    무방향 그래프: 방향성이 없는 그래프  
    완전 그래프: 오른쪽과 같이 정점이 모두 연결된 그래프  
    
    ![Untitled](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fpo5pP%2FbtrSJW6oZlT%2FJfMU9g3MxYg92dw3j1I240%2Fimg.png)
    
- 방향 그래프: 방향성이 있는 그래프
    
    ![Untitled](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fpo5pP%2FbtrSJW6oZlT%2FJfMU9g3MxYg92dw3j1I240%2Fimg.png)
    

- 가중치 그래프: 간선에 가중치를 담아서 표현
    
    ![Untitled](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbGytlo%2FbtrSM4WV6xA%2F6CTrSqGCYT8wXVxJTVu2Zk%2Fimg.png)
    
- 부분 그래프: 일부 정점과 간선으로 구성된 그래프
    
    ![Untitled](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FlyDJp%2FbtrSKuBXz7m%2F1qqZ5Nsf2B2hZP51izzSR0%2Fimg.png)

<br>

## 그래프의 집합 표현

정점의 집합을 V(G), 간선의 집합을 E(G)로 표현  
방향성이 없는 경우 괄호()로 묶음  
방향성이 있는 경우 부등호<>로 묶고, 간선의 시작 부분을 먼저 표현  

<br>

## 그래프를 구현하는 두 가지 방법

1. 인접 행렬 기반 그래프: 정방행렬을 활용
2. 인접 리스트 기반 그래프: 연결 리스트를 활용

![Untitled](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcBZQjD%2FbtrSSMaaaag%2FmLkB1Q2h8rijIE0KZ43vL0%2Fimg.png)

<br>

---

# 14-2 인접 리스트 기반의 그래프 구현

딕셔너리로 구현

```python
k = 4 # k는 간선의 수
graph = {}

for _ in range(k):
    x, y = map(int, input().split()) # 정수 입력
    if x not in graph.keys(): # x가 키가 아니면
        graph[x] = set([y]) # 값에 넣음
    else: 
        graph[x].add(y)
    if y not in graph.keys():
        graph[y] = set([x])
    else:
        graph[y].add(x)
```

<br>

---

# 14-3 그래프의 탐색

## 깊이 우선 탐색(Depth First Search)

연결된 정점 중 하나를 선택해서 탐색하는 방법  
먼저 시작 정점에서부터 정점을 하나씩 선택하여 탐색을 시작  
스택 이용  

![Untitled](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbofeS2%2FbtrSTxcTilq%2FiZhFK6qV0KXkMgXkODAozK%2Fimg.png)

```python
# 스택으로 구현한 깊이 우선 탐색

class myGraph:
  def __init__(self):
    self.graph = {}

  def addInfo(self, startV, endVs):
    self.graph[startV] = endVs
  
  def addEdge(self, startV, endV): # 간선 추가
    self.graph[startV].append(endV)
  
  def addVertex(self, V): # 정점 추가
    self.graph[V] = []

  def dfs(self, startV): # 깊이 우선 탐색
    s = [startV]
    visited = [] # 방문한 노드를 넣을 리스트
    while s:
      now = s.pop()
      if now not in visited: # 방문하지 않은 노드라면
        visited.append(now)
        s.extend(self.graph[now][::-1])
    return visited

g = myGraph()
g.addInfo( 'A', ['B',  'E',  'I'])
g.addInfo( 'B', ['A',  'C'])
g.addInfo( 'C', ['B',  'D'])
g.addInfo( 'D', ['C'])
g.addInfo( 'E', ['A',  'F',  'H'])
g.addInfo( 'F', ['E',  'G'])
g.addInfo( 'G', ['F'])
g.addInfo( 'H', ['E'])
g.addInfo( 'I', ['A',  'J'])
g.addInfo( 'J', ['I'])

print(g.dfs('A'))
# ['A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J']
```

<br>

## 너비 우선 탐색(Breadth First Search)

연결된 정점을 모두 탐색하면서 진행하는 방법  
탐색한 정점 순서대로 주변을 탐색함  
큐 이용  

```python
# 큐로 구현한 너비 우선 탐색

class myGraph:
  def __init__(self):
    self.graph = {}

  def addInfo(self, startV, endVs):
    self.graph[startV] = endVs
  
  def addEdge(self, startV, endV): # 간선 추가
    self.graph[startV].append(endV)
  
  def addVertex(self, V): # 정점 추가
    self.graph[V] = []
  
  def bfs(self, startV): # 너비 우선 탐색
    q = [startV]
    visited = [startV] # 방문한 노드를 넣을 리스트
    while q:
      now = q.pop(0) # 큐의 맨 앞의 노드를 꺼냄
      for nextV in self.graph[now]:
        if nextV not in visited:
          q.append(nextV)
          visited.append(nextV)
    return visited

g = myGraph()
g.addInfo( 'A', ['B',  'E',  'I'])
g.addInfo( 'B', ['A',  'C'])
g.addInfo( 'C', ['B',  'D'])
g.addInfo( 'D', ['C'])
g.addInfo( 'E', ['A',  'F',  'H'])
g.addInfo( 'F', ['E',  'G'])
g.addInfo( 'G', ['F'])
g.addInfo( 'H', ['E'])
g.addInfo( 'I', ['A',  'J'])
g.addInfo( 'J', ['I'])

print(g.bfs('A'))
# ['A', 'B', 'E', 'I', 'C', 'F', 'H', 'J', 'D', 'G']
```

<br>

---

# 14-4 최소 비용 신장 트리

- 단순 경로
    - 정점에서 정점으로 이동하는 경로
    - 중복된 간선을 포함하지 않음
- 사이클
    - 단순 경로이면서 시작과 끝이 같은 경로
    - 사이클이 형성되면 폐구간이 만들어짐

<br>

## 최소 비용 신장 트리(MST)

- 신장 트리의 특징  
    그래프의 모든 정점이 간선에 의해서 하나로 연결되어 있음  
    그래프 내에서 사이클을 형성하지 않음  
    
- 최소 비용 신장 트리  
    신장 트리의 모든 간선의 가중치 합이 최소인 그래프  
    
    1. 크루스칼 알고리즘
        1.  가중치를 기준으로 간선을 정렬한 후에 MST가 될 때까지 간선을 하나씩 선택 또는 삭제해 나가는 방식
    2. 프림 알고리즘
        1.  하나의 정점을 시작으로 MST가 될 때까지 트리를 확장해 나가는 방식

<br>

## 크루스칼 알고리즘1

1. 간선의 가중치를 오름차순으로 정렬
2. 오름차순 순서대로 간선을 연결(추가)
3. 추가할 때 간선이 사이클을 형성하거나 신장 트리가 완성되었다면 추가하지 않음

<br>

## 크루스칼 알고리즘2

1. 간선의 가중치를 내림차순으로 정렬
2. 내림차순 순서대로 간선을 삭제
3. 삭제할 때 정점이 독립되거나(연결된 간선이 없음) 신장 트리가 완성되었다면 삭제하지 않음
4. 간선의 수가 정점의 수보다 하나 적을 때 MST 완성

<br>

## 구현
```python
graph=[(1,2,13),(1,3,5),(2,4,9),(3,4,15),(3,5,3),(4,5,1),(4,6,7),(5,6,2)]
graph.sort(key = lambda x: x[2]) # 가중치로 간선 정렬 (정점1, 정점2, 가중치)

mst=[]
n=6 # 정점 개수
p=[0] # 상호배타적 집합

for i in range(1,n+1):
    p.append(i) # 부모 테이블상에서 부모를 자기 자신으로 초기화

# 특정 원소가 속한 집합을 찾음
def find(u):
    if u != p[u]:
        p[u] = find(p[u]) # 루트 노드를 찾을 때까지 재귀 호출
    return p[u]

# 두 원소가 속한 집합을 합침
def union(u, v):
    root1 = find(u)
    root2 = find(v)
    p[root2] = root1

tree_edges = 0 # 간선 개수
mst_cost = 0 # 가중치 합

while True:
    if tree_edges == n-1: # 간선의 수가 정점의 수보다 하나 적으면
        break
    u, v, wt =graph.pop(0)
    if find(u) != find(v): # u와 v가 서로 다른 집합에 속해 있으면(사이클 발생 X)
        union(u, v)
        mst.append((u, v)) 
        mst_cost += wt
        tree_edges += 1

print('최소신장트리: ',mst)
# [(4, 5), (5, 6), (3, 5), (1, 3), (2, 4)]

print('최소신장트리 가중치:', mst_cost)
# 20
```
<br>
Ch 7. 큐와 Ch 13. 테이블과 해쉬를 제외하면 정리가 끝났습니다.  
파이썬으로 자료구조를 공부하니까 더 재밌네요 ㅎㅎ  

<br>

