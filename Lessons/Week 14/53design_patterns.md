# 04/18/22: Introduction to Design Patterns

## Design Patterns
- Each pattern describes a problem which occurs over and over again in our environment, and then describes the core of the solution to that problem, in such a way that you can use this solution a million times over, without ever doing it the same way twice

### Parts of the design pattern:
- **Name**: describes problem, solution, consequences in a single word or two. allows us to develop vocab to discuss with peers, documentation, etc.
- **Problem solved**: when to apply, problem + context
- **Solution**: abstract description of pattern, should be adaprted to different situations
- **Consequences**: trade-offs

## Micro Patterns 
### Most-wanted holder
- **Name**: most-wanted holder
- **Problem**: what to find the "most wanted" element of a collection 
- **Solution**: 
    - initialize most-wanted holder to the first element in the collection
    - compare every other element to value in most-wanted holder
    - update if new value is better
```cpp
std::vector<Thing> things;
Thing most_wanted = things.at(0);
for (size_t i = 0; i < things.size(); i++) {
    if (things.at(i) > most_wanted) {
        most_wanted = things.at(i);
    }
}
```

### One-way flag
- **Name**: One-way flag
- **Problem**: want to know if a property is true/false for every element in a collection
- **Solution**: 
    - initialize a boolean to one value
    - traverse the whole collection
    - setting the boolean to the other value if an element violates the property 
```cpp
std::vector<Thing> things;
bool all_valid = true;
for (auto thing : things) {
    if (!thing.Value()) {
        all_valid = false;
        break;
    }
}
```

### Follower
- **Name**: Follower
- **Problem**: want to compare adjavent elements of collection
- **Solution**: 
    - iterate through a collection
    - set the value of some follower variable to the current element as the last step
```cpp
std::vector<Thing> things;
Thing follower = things.at(0);
bool collection_in_order = true;
for (auto thing : things) {
    // note first comparison will be a self comparison in this implementation
    if (follower > thing) {
        collection_in_order = false;
    }
    follower = thing;
}
```

## Strategy Pattern
- Intent: define a family of algorithms, encapsulate each one, make them interchangable
- Use when:
    - Many related classes differ only in their behavior 
    - You need different variants of an algorithm
    - An algorithm uses data that clients shouldn't know about
    - Encapsulate the algorithm data from the client
    - Class defines multiple behaviors and these are implemented using conditionals 

![Image](/Images/strategy_pattern.png)

Ex: Bird class has Speak() function that is implemented by every child class because each bird makes a unique sound. But what if some birds make the same sound? (Rubber Duck makes no quack, Mallard Duck makes loud quack...) **Turn this behavior into its own abstract class: HAS-A behavior**

![Image](/Images/strategy_pattern2.png)
