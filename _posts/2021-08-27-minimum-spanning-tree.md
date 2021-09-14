---

layout: post

title: 최소 신장 트리(MST) 크러스컬(Kruskal), 프림(Prim) 알고리듬; 백준 1197 최소 스패닝 트리(Python)

categories: [Algorithm]

tags: [Algorithm, Graph, MST, Python]

filename: 2021-08-27-minimum-spanning-tree.md

draft: 2021-08-27 09:38:00

date: 2021-09-14 21:52:00

modified: 2021-09-14 21:52:00

---


## 최소 신장 트리(Minimum Spanning Tree, MST)

**신장 트리(Spanning Tree)**란 그래프의 모든 정점(vertex)을 잇는 트리입니다. 신장(伸長)은 '길게 늘리다' 라는 의미로 그래프 내에서 모든 정점으로 쭉 뻗어나간 트리의 모양을 떠올리면 됩니다. 하나의 그래프에서 여러 개의 신장 트리가 존재할 수 있습니다.

![https://upload.wikimedia.org/wikipedia/commons/thumb/d/d2/Minimum_spanning_tree.svg/300px-Minimum_spanning_tree.svg.png](https://upload.wikimedia.org/wikipedia/commons/thumb/d/d2/Minimum_spanning_tree.svg/300px-Minimum_spanning_tree.svg.png)

최소 신장 트리(Minimum Spanning Tree, MST)

신장 트리 중에서 모든 간선(edge)의 가중치(weight)의 합이 가장 작은 신장 트리를 **최소 신장 트리(Minimum Spanning Tree, MST)**라고 합니다. 마찬가지로 하나의 그래프에서 여러개의 최소 신장 트리가 존재할 수 있습니다.

![https://upload.wikimedia.org/wikipedia/commons/thumb/c/c9/Multiple_minimum_spanning_trees.svg/220px-Multiple_minimum_spanning_trees.svg.png](https://upload.wikimedia.org/wikipedia/commons/thumb/c/c9/Multiple_minimum_spanning_trees.svg/220px-Multiple_minimum_spanning_trees.svg.png)

여러 개 존재할 수 있는 MST


### Cut Property

MST를 찾는 알고리듬을 이해하는데는 MST의 **컷 프로퍼티(cut property)**를 이해할 필요가 있습니다. 컷 프로퍼티란 ‘그래프의 임의의 컷 세트(cut-set)에서 가중치가 가장 작은 간선은 MST에 포함’되는 특성입니다.


#### 컷(cut)과 컷 세트(cut-set)

어떤 그래프를 서로소(disjoint)인 두 하위 집합으로 나누는 행위를 **컷(cut)**이라고 합니다. 간단하게 말하면 그래프를 둘로 쪼개는 행위입니다. 그리고 이렇게 나누어진 두 그룹을 이어주는 모든 간선을 **컷 세트(cut-set)**라고 합니다.

![https://upload.wikimedia.org/wikipedia/commons/thumb/0/02/Min-cut.svg/220px-Min-cut.svg.png](https://upload.wikimedia.org/wikipedia/commons/thumb/0/02/Min-cut.svg/220px-Min-cut.svg.png)

컷 세트(cut-set)

위 그래프에서 빨간색 간선 2개가 컷 세트(cut-set)입니다. 컷 세트에 포함된 모든 간선을 끊어주면(빨간 간선을 모두 끊어주면) 그래프가 둘로 나뉘어 지겠죠. 반대로 컷 세트에 포함된 간선 중 하나만 연결되어도 두 그룹은 이어지게됩니다.


## MST 알고리듬의 기본 원리

컷 프로퍼티라는 속성을 이용해서 MST를 찾는 알고리듬은 다음과 같습니다. 일종의 그리디(Greedy) 알고리듬입니다.



1. 그래프에 있는 간선을 하나 확인한다.
2. 이 간선이 MST에 포함되는지 검사한다.
    1. 이 때 **컷 프로퍼티(cut property)를 사용**한다.
    2. MST에 포함되는 간선이면 MST에 추가하고 아니면 무시한다.
3. MST의 모든 변을 찾지 못했다면 다시 1번으로 돌아가서 반복한다.
    3. N-1개(N은 노드 개수)의 간선을 찾으면 모두 찾은 것이니 종료한다.

컷 프로퍼티를 사용한다는 것의 의미는 다음과 같습니다.



* 컷 프로퍼티: 그래프의 임의의 컷 세트(cut-set)에서 가중치가 가장 작은 간선은 MST에 포함된다.
* → 가중치가 가장 작은 간선은 무조건 MST에 포함된다.
* → MST를 만들 수 있는 간선 후보 중 가중치가 가장 작은 것을 선택해나가면 된다. (그리디)


### 대표적인 MST 알고리듬

지금까지 MST의 특성인 컷 프로퍼티로 인해 ‘그래프에서 가중치가 가장 작은 간선을 선택하다 보면 MST가 완성된다’는 기본 원리를 파악했습니다. 그럼 이제부터 본격적으로 MST 간선 후보를 선택하는 알고리듬을 알아보겠습니다. 크게 2가지 방식이 있습니다.



1. 크러스컬 알고리듬(Kruskal’s algorithm)
2. 프림 알고리듬(Prim’s algorithm)

**크러스컬 알고리듬(Kruskal’s algorithm)**은 그래프 전체에서 가중치가 가장 작은 간선부터 차례대로 **합치는 방식**이고, **프림 알고리듬(Prim’s algorithm)**은 하나의 노드에서 시작해서 MST에 포함되는 간선으로 **뻗어나가는 방식**입니다.

![https://upload.wikimedia.org/wikipedia/commons/b/bb/KruskalDemo.gif](https://upload.wikimedia.org/wikipedia/commons/b/bb/KruskalDemo.gif)

크러스컬 알고리듬(Kruskal’s algorithm) 예시

![https://upload.wikimedia.org/wikipedia/commons/9/9b/PrimAlgDemo.gif](https://upload.wikimedia.org/wikipedia/commons/9/9b/PrimAlgDemo.gif)

프림 알고리듬(Prim’s algorithm) 예시


## 크러스컬 알고리듬(Kruskal’s algorithm)

크러스컬 알고리듬의 핵심은 그래프를 합쳐나가는 것입니다. 그래프 합치기를 위해서 사용되는 자료구조가 **서로소 집합(disjoint-set)** 또는 **합집합 찾기(union-find)**라고 불리는 자료구조입니다.


### 서로소 집합(disjoint-set), 합집합 찾기(union-find) 자료구조

**서로소 집합(disjoint-set)** 또는 **합집합 찾기(union-find)**라고 불리는 자료구조는 ‘서로소 부분 집합’으로 이루어진 원소들을 저장하고 조작할 수 있는 자료구조 입니다. 개념을 설명하기에는 서로소 집합(disjoint-set) 이라는 이름이, 코드를 설명하기에는 합집합 찾기(union-find) 라는 이름이 이해하기 쉬워서 둘 다 표기하였습니다.

서로소 집합 자료구조에는 3가지의 연산이 있습니다.



1. **MakeSet(x)**
    1. x라는 원소 하나를 가지는 새로운 집합을 생성합니다.
2. **Find(x)**
    2. 어떤 원소 x가 포함된 집합에서 ‘대표 원소(루트 노드)’를 반환합니다.
3. **Union(x, y)**
    3. x가 포함된 집합과 y가 포함된 집합을 하나의 집합으로 합칩니다.

서로소 집합 자료구조를 이해하기 쉽게 비유하자면, 꼬리잡기 놀이와 비슷합니다. 맨 처음에는 한 명이서 시작해서(MakeSet) 만나면 서로 합쳐집니다(Union). 가장 앞에 있는 사람은 해당 집합의 대표라고 할 수 있죠(Find가 반환하는 루트 노드).


### 서로소 집합을 사용한 크러스컬 알고리듬



1. 서로소 집합의 MakeSet을 사용해 그래프의 모든 노드를 별도의 그래프 집합으로 만듭니다.
2. 그래프의 간선을 가중치의 오름차순으로 정렬한 S 배열을 만듭니다.
3. MST가 완성될 때까지 다음을 반복합니다.
    1. S에서 가장 가중치가 작은 간선 e를 가져옵니다. (S에서는 e 삭제)
    2. Find를 사용해 e가 연결하는 두 노드가 같은 집합에 포함되는지 확인합니다.
        1. 두 노드 u, v에 대해 Find(u) != Find(v)면 두 집합을 Union(u, v) 연산으로 합치고 e를 MST에 추가합니다.
        2. Find(u) == Find(v) 이면 그냥 넘어갑니다.
    3. S가 비거나 MST에 포함되는 N-1개의 간선(N은 노드 개수)을 모두 찾으면 종료합니다.


### 크러스컬 알고리듬의 시간 복잡도

크러스컬 알고리듬의 시간 복잡도는 **O(E log E)** **= O(E log V)**입니다. 자세한 시간 복잡도는 다음과 같습니다. V는 정점의 개수, E는 간선의 개수 입니다.



1. MakeSet: O(V)
2. 간선 정렬: O(E log E)
3. 모든 간선에 대해 Find, Union: O(E) * O(1)
    1. union by rank와 path compression이라는 기법으로 Find와 Union의 시간 복잡도를 O(1)까지 낮출 수 있습니다. 간단히 설명하면, 원소가 대표를 바로 가리키게 해서 일일히 대표에 대한 정보를 업데이트하거나 찾을 필요가 없도록 하면 됩니다.


## 프림 알고리듬(Prim’s algorithm)

프림 알고리듬의 핵심은 그래프를 뻗어나가는 것입니다. 가중치가 가장 작은 간선을 선택해 나간다는 점에서 다익스트라 알고리듬과도 유사한 부분이 있습니다.



1. 아무 노드나 골라서 트리를 만듭니다. (루트 노드)
2. MST가 완성될 때까지 다음을 반복합니다.
    1. 현재 트리를 성장시킬 수 있는 간선(아직 트리에 포함되지 않는 노드와 연결하는 간선) 중 가중치가 가장 작은 값을 선택합니다.
    2. S가 비거나 MST에 포함되는 N-1개의 간선(N은 노드 개수)을 모두 찾으면 종료합니다.


### 프림 알고리듬의 시간 복잡도

프림 알고리듬의 시간 복잡도는 어떤 자료구조를 사용하는지에 따라 다릅니다. 가장 가중치가 작은 간선을 검색하는데 자료구조의 영향을 많이 받습니다. 결론적으로 인접 행렬을 사용하는 경우 O(V²), 힙이나 인접 리스트를 사용하는 경우 O(E log V), 피보나치 힙을 사용하는 경우엔 O(E + V log V)의 시간 복잡도를 가집니다.

일반적으로 힙을 사용해 구현하므로 크러스컬 알고리듬과 동일하게 **O(E log V)**라고 기억하면 되겠습니다.


## 크러스컬 알고리듬 vs 프림 알고리듬

지금까지 MST를 찾는 알고리듬인 크러스컬 알고리듬과 프림 알고리듬에 대해 알아보았습니다. 그럼 두 알고리듬 모두 시간 복잡도가 같은데, 어떤 알고리듬을 선택하는 것이 좋을까요?

**간선이 적은 경우 크러스컬 알고리듬**을, **간선이 많은 경우 프림 알고리듬**을 선택하는 것이 좋습니다. 크러스컬 알고리듬은 시작 전 모든 간선을 정렬해서 사용하고, 프림 알고리듬은 그때그때 주변 간선들을 찾아서 사용하기 때문이죠. 하지만 구현에 따라 실제로 소요되는 시간은 다를 수 있습니다.


## 구현 코드(Python)

[백준 1197번: 최소 스패닝 트리](https://www.acmicpc.net/problem/1197)를 크러스컬과 프림으로 구현한 코드입니다. 문제는 MST의 가중치의 합을 구하는 문제라 MST의 모든 간선을 리스트에 추가하는 코드는 주석으로 남겨놓았습니다.

<script src="[https://gist.github.com/MiJey/b524564db3963fba9e38d1c8705bca00.js](https://gist.github.com/MiJey/b524564db3963fba9e38d1c8705bca00.js)">

</script>

<script src="[https://gist.github.com/MiJey/82f68cc4112df1fba1e28e8f91a71b00.js](https://gist.github.com/MiJey/82f68cc4112df1fba1e28e8f91a71b00.js)">

</script>
