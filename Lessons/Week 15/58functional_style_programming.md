# 04/26/22: Functional-Style Programming

## Terminology
- **Higher-order functions**: function that operates or uses another function
- **First class functions**: functions can be stored as variables
```cpp
std::function<bool (const Movie&)> filter;

...

if (filter(movie)) {
    filtered_movies.push_back(movie);
}
```

## Functional-style programming
- Solve problems by composing functions rather than loops 
- Reusable higher-order functions
```cpp
std::vector<Movie> filtered_movies;
std::copy_if(movies.begin(),
            movies.end(),
            std::back_inserter(filtered_movies),
            [](auto& m) { return m.release_year < 1990; });
```

- Strict funtional languages: Haskell, OCaml