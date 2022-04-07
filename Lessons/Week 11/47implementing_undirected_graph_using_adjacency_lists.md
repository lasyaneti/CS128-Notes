# 04/06/2022: Implementing an undirected graph type using adjacency lists

## What we are implementing
```cpp
template <typename T>
class SimpleUndirectedGraph {
public:
    SimpleUndirectedGraph(size_t no_v);
    void AddEdge(size_t v, size_t, w);
    bool IdAdjacent(size_t v, size_t w);

    std::pair<std::list<size_t>::const_iterator, std::list<size_t>::const_iterator> Asj(size_t v) const;
    size_t NoVerticies() const { return no_verticies_; }
    size_t NoEdges() const { return no_edges_; }

    template <typename R>
    friend std::ostream& operator<<(std::ostream& os, const SimpleUndirectedGraph<R>& sug);

private:
    std::vector<T> verticies_;
    std::vector<std::list<size_t>> adj_;
    size_t no_verticies_;
    size_t no_edges_;
};
```

## Construction
```cpp
template <typename T>
SimpleUndirectedGraph<T>::SimpleUndirectedGraph(size_t no_v) : no_verticies_(no_v), no_edges_(0) {
    verticies_.resize(no_v);
    adj_.resize(no_v);
}
```

## Adding edges
```cpp
template <typename T>
void SimpleUndirectedGraph<T>::AddEdge(size_t v, size_t w) {
    if (IsAdjacent(v, w) || IsAdjacent(w, v)) {
        throw std::invalid_argument("edge already exists in graph");
    }
    adj_.at(v).push_back(w);
    adj_.at(w).push_back(v);
    no_edges += 1;()
}
```

## Are we neighbors
```cpp
template <typename T>
bool SimpleUndirectedGraph<T>::IsAdjacent(size_t v, size_t w) {
    // use (find) function from standard libary list
    return (std::find(adj_.at(v).cbegin(), adj_.at(v).cend(), w) != adj_.at(v).cend());
}
```

### Iterators
- Some way to move through data similarly to how we did in an array
- Sequence of nodes

## Who are our neighbors
```cpp
template <typename T>
std::paid<std::list<size_t>::const_iterator, std::list<size_t>::const_iterator> SimpleUndirectedGraph<T>::Adj(size_t v) const {
    return std::make_pair(adj_.at(v).cbegin(), adj_.at(v).cend());
}
```