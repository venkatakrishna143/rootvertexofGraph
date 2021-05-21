# rootvertexofGraph
CHAR_SIZE = 128
class Graph:
    def __init__(self, N, edges):
        self.adj = [[] for _ in range(N)]
 
        for edge in edges:
            self.addEdge(edge[0], edge[1])
 
    def addEdge(self, u, v):
        self.adj[u].append(v)
 
 
def DFS(graph, v, discovered):
    discovered[v] = True        # mark the current node as discovered
 
    for u in graph.adj[v]:
        if not discovered[u]:   # `u` is not discovered
            DFS(graph, u, discovered)
 
 
def findRootVertex(graph, N):
 
    discovered = [False] * N
 
    v = 0
    for i in range(N):
        if not discovered[i]:
            DFS(graph, i, discovered)
            v = i
 
    discovered[:] = [False] * N
 
    DFS(graph, v, discovered)
 
    for i in range(N):
        if not discovered[i]:
            return -1
 
    return v
 
 
if __name__ == '__main__':
 
    edges = [(0, 1), (1, 2), ( 2, 3), ( 3, 0), ( 4, 3), ( 4, 5), ( 5, 0)]
 
    N = 6
 
    graph = Graph(N, edges)
 
    root = findRootVertex(graph, N)
 
    if root != -1:
        print("The root vertex is", root)
    else:
        print("The root vertex does not exist")
