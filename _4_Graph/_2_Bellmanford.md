struct edge {  
    int from, to, weight;  
  
    edge() { from = to = weight = 0; }  
  
    edge(int from, int to, int weight) :  
            from(from), to(to), weight(weight) {  
    }  
  
    bool operator<(const edge &other) const {  
        return weight > other.weight;  
    }  
};  
  
vector<edge> edgeList;  
  
//O(V*E)  
void bellmanford(int n, int src, int dest = -1) {  
    vector<int> dis(n + 1, oo), prev(n + 1, -1);  
    dis[src] = 0;  
    bool negativeCycle = false;  
    int last = -1, tmp = n;  
    while (tmp--) {  
        last = -1;  
        for (edge e: edgeList)  
            if (dis[e.to] > dis[e.from] + e.weight) {  
                dis[e.to] = dis[e.from] + e.weight;  
                prev[e.to] = e.from;  
                last = e.to;  
            }  
        if (last == -1)  
            break;  
        if (tmp == 0)  
            negativeCycle = true;  
    }  
    if (last != -1) {  
        for (int i = 0; i < n; i++)  
            last = prev[last];  
        vector<int> cycle;  
        for (int cur = last; cur != last || cycle.size() > 1; cur =  
                                                                      prev[cur])  
            cycle.push_back(cur);  
        reverse(cycle.begin(), cycle.end());  
    }  
    vector<int> path;  
    while (dest != -1) {  
        path.push_back(dest);  
        dest = prev[dest];  
    }  
    reverse(path.begin(), path.end());  
}