# Binary Tree
## Traversal Methods O(N)
PreOrder: Root Left Right
InOrder: Left Root Right
PostOrder: Left Right Root
Level-Order: BFS

## Types
Full: 除了Leaf以外其他Node都有兩個Child
Complete: 只有最後一層右側不完整
Perfect: 完整

## Right Subtree Height:
Full: N-1
Complete: N-2
Perfect: N-1

## Binary Search Tree (BST)
InOrder會小到大輸出

Lookup O(logN)
Insert O(logN)
Delete O(logN)

# Heap

條件:
1. 是Complete Binary Tree.
2. Parent永遠會 <= / >= Child

# Binary Heap
Lookup O(N)
Insert O(1)
Find Max O(1)
Delete Min O(logN)

# Min Heap / Max Heap

# Min-Max Heap
Insert O(logN)
Delete O(logN)

# Union-Find
```c
map<int,int> parent;
map<int,int> rank;

//init
void init(int n) {
    for(int i = 1;i<=n;i++) {
        parent[i] = i;
        rank[i] = 0;
    }    
}

//find the root of x
int find(int x) {
    if(parent[x] != x)
        return parent[x] = find(parent[x]);
    return x;
}

//union a and b
void unionSet(int a, int b) {
    int r1 = find(a);
    int r2 = find(b);

    if(r1 == r2) {
        return;
    }
	
    if(rank[r1] < rank[r2]) {
        parent[r1] = r2;
    } else {
        parent[r2] = r1;
    }
	
    if(rank[r1] == rank[r2]) {
        rank[r1]++;
    }
}
```

# Kruskal Algorithm
## Find Minimum Span Tree
```c
//undirected edges
struct Edge {
    int a, b, w;
};

vector<Edge> edges;
```
```c
//kruskal start
sort(edges.begin(), edges.end(), [](Edge e1, Edge e2) {
    return e1.w < e2.w;
});
        
vector<Edge> mst;
for(Edge e : edges) {
    int r1 = find(e.a);
    int r2 = find(e.b);
    if (r1 != r2) {
        mst.push_back(e);
        unionSet(r1, r2);
    }
}
```
# Prim's Algorithm

## Find Minimun Span Tree
```c
//adjacent graph
struct Edge {
    int b;
    int w;
    bool operator>(const Edge& other) const {
        return w > other.w;
    }
};

vector<vector<Edge>> graph(N);
```
```c
//prim start
vector<Edge> mst;

void prim(int start, int N) {
    vector<bool> visited(N, false);
    priority_queue<Edge, vector<Edge>, greater<>> pq;

    for (Edge e : graph[start]) {
        pq.push(e);
    }
    visited[start] = true;

    while (!pq.empty()) {
        Edge edge = pq.top();
        pq.pop();

        if (visited[edge.b]) 
            continue;
        
        mst.push_back(edge);
        visited[edge.b] = true;

        for (Edge e : graph[edge.b]) {
            if (!visited[e.b]) {
                pq.push(e);
            }
        }
    }
}
```
```c
//usage
start(0, N);
```

# Dijkstra Algorithm

## Find Shortest Path
```c
//adjacent graph
struct Edge {
    int b,
    int w;
        
    bool operator>(const Edge& other) const {
        return w > other.w;
    }
}

vector<vector<Edge>> graph(N);
```
```c
//dijkstra start
vector<int> dijkstra(int source, int N) {
    vector<int> distance(N, 2147483647);
    distance[source] = 0;

    priority_queue<Edge, vector<Edge>, greater<Edge>> pq;
    pq.push({0, source});

    while (!pq.empty()) {
        Edge edge = pq.top();
        pq.pop();

        if (edge.w > distance[edge.b])
            continue;

        for (Edge e : graph[edge.b]) {
            int new_dist = edge.w + e.w;
            if (new_dist < distance[e.b]) {
                distance[e.b] = new_dist;
                pq.push({new_dist, e.b});
            }
        }
    }

    return distance;
}
```
#### Usage
```c
//usage
int dist = dijkstra(1,N)[4]; //shortest path between 1 and 4
```