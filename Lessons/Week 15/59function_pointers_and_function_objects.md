# 04/27/22: Function Pointers and Function Objects

## Set-up
```cpp
enum class Rating { kR, kPG, kPG13, kR};
struct Movie {
    std::string title;
    std::string director;
    Rating rating;
    unsigned int release_year; 
}
```

Declarative approach seems faster than imperitive, how can we move forward from here?

## Function pointers
- Printing a function without the call operator prints an ADDRESS!! So we can make a pointer to this address of the function
```cpp
// function_return_type (*PointerName)(function_parameter_list_types) = initializer;

bool (*MySillyFunctionPtr)(int, int) = MySillyFunction;

MySillyFunctionPtr(1, 2); // works the same as MySillyFunction(1, 2)
```
- **Advantage**: minimal syntactic overhead
- **Disadvantage**: doesn't retain state within a scope

## Function objects
- Any type that implements the call operator (operator())
- This creates callable objects 
    - **Advantage**: doesn't retain state within a scope
    - **Disadvantage**: minimal syntactic overhead

```cpp
class ReleasedBefore {
public:
    ReleasedBefore(unsigned int year): year_(year) { }
    bool operator()(const Movie& movie) const { return movie.release_year < year_; }
private:
    unsigned int year_;
}
```

## Defining higher-order functions that accept function pointers AND function objects
```cpp
std::vector<Movie> FilterMovies(const std::vector<Movie>& movies, std::function<bool (const Movie&)> filter) {
    std::vector<Movie> filtered_movies; 
    for (auto& movie : movies) {
        if (filter(movie)) {
            filtered_movies.push_back(movie);
        }
    }
    return filtered_movies;
}
```