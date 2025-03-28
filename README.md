# C++ Syntax & Modern Features Cheatsheet

> This comprehensive cheatsheet covers essential C++ syntax and modern features for general programming and technical interviews. It includes standard library components, data structures, algorithms, and language features from C++11 through C++20 with time complexity information where relevant.

## 1. Basic Syntax & Control Flow

> The foundation of any C++ program includes headers, control structures, and basic syntax elements.

### 1.1 Common #include Statements
> Essential headers for accessing the C++ Standard Library components:
```cpp
#include <iostream>     // std::cin, std::cout
#include <vector>       // std::vector
#include <string>       // std::string
#include <algorithm>    // std::sort, std::min, std::max, etc.
#include <map>          // std::map
#include <unordered_map>// std::unordered_map
#include <set>          // std::set
#include <unordered_set>// std::unordered_set
#include <queue>        // std::queue, std::priority_queue
#include <stack>        // std::stack
#include <list>         // std::list
#include <deque>        // std::deque
#include <numeric>      // std::accumulate
#include <random>       // std::mt19937, std::uniform_int_distribution
#include <memory>       // smart pointers
#include <functional>   // std::greater, std::less
#include <bit>          // C++20 bit operations (popcount, rotl, etc.)
#include <optional>     // C++17 std::optional
#include <variant>      // C++17 std::variant
#include <any>          // C++17 std::any
#include <thread>       // std::thread
#include <mutex>        // std::mutex, std::lock_guard
#include <future>       // std::async, std::future
#include <filesystem>   // C++17 std::filesystem
#include <sstream>      // std::stringstream
```

### 1.2 Switch Case
> A multi-way branch statement that tests a value against multiple constant cases:
```cpp
int value = 2;
switch (value) {
  case 1:
    // ...
    break;
  case 2:
    // ...
    break;
  default:
    // ...
    break;
}
```
- Expression must be integral or enum type
- Each case label must be a constant expression

## 2. Strings in C++

> C++ provides robust string handling through the `std::string` class, offering numerous manipulation functions.

### 2.1 std::string Basics
> Various ways to create and initialize strings:
```cpp
std::string s1;                    // empty
std::string s2("Hello");           // from const char*
std::string s3 = "World";          // copy init
std::string s4(s3);                // copy constructor
std::string s5(5, 'X');            // "XXXXX"
```

**Common String Functions and Their Time Complexities:**

| Function | Description | Time Complexity |
|----------|-------------|-----------------|
| `s.size()`, `s.length()` | Returns string length | O(1) |
| `s.empty()` | Checks if string is empty | O(1) |
| `s.clear()` | Clears the contents | O(n) |
| `s.push_back(char c)`, `s.pop_back()` | Add/remove character at end | O(1) amortized |
| `s.append(const std::string&)` | Append string | O(m) |
| `s += otherString` | Concatenation | O(m) |
| `s.substr(pos, count)` | Substring from pos of length count | O(count) |
| `s.find(str, pos)` | Find substring, returns `std::string::npos` if not found | O(n*m) worst-case |
| `s.replace(pos, len, str)` | Replace portion [pos, pos+len) with str | O(n + m) |
| `s.insert(pos, str)` | Insert str at position pos | O(n + m) |
| `s.erase(pos, len)` | Erase len chars starting at pos | O(n) |
| `std::stoi(s)`, `std::stoll(s)` | Convert string to numeric types | O(n) |
| `std::to_string(val)` | Convert numeric to string | O(log n) |

### Useful Examples
```cpp
  // size_t used for operating with size
  size_t pos = text.find("world");
    if (pos != std::string::npos) {
        std::cout << "Found at index: " << pos << std::endl;
    } else {
        std::cout << "Not found" << std::endl;
    }
```

### 2.2 String Streams
> String streams provide an easy way to perform string conversions and formatting, similar to Java's StringBuffer:
```cpp
#include <sstream>

std::stringstream ss;
ss << "Hello " << 123;
std::string out = ss.str();  // "Hello 123"

// Clearing
ss.str(std::string());
ss.clear();
```

## 3. Modern C++: Initialization & Type Inference

> Modern C++ (C++11 and beyond) introduced cleaner ways to initialize variables and infer types automatically.

### 3.1 Uniform Initialization (Brace Initialization)
> A consistent syntax for initializing objects of all types, helping prevent narrowing conversions:
```cpp
int x{10};
double d{3.14};
std::vector<int> v{1, 2, 3};
```

### 3.2 auto Keyword
> Lets the compiler deduce the type from the initializer expression, reducing verbosity:
```cpp
auto i = 10;             // int
auto f = 3.14;           // double
auto s = std::string("hi");
```

### 3.3 Range-based for Loop
> Simplifies iteration over containers and arrays:
```cpp
std::vector<int> nums{1, 2, 3};
for (auto n : nums) {
    std::cout << n << " ";
}

// If modifying elements, use reference:
for (auto& n : nums) {
    n *= 2;
}
```

### 3.4 Structured Bindings (C++17)
> Allows decomposing objects like pairs, tuples, and structs into individual variables:
```cpp
std::pair<int, std::string> p{1, "one"};
auto [num, str] = p;         // structured binding
std::cout << num << " " << str;

std::map<int, std::string> m{{1, "one"}, {2, "two"}};
for (auto const& [k, v] : m) {
    std::cout << k << " => " << v << "\n";
}
```

## 4. Math & Utility Functions

> C++ provides a comprehensive set of mathematical and utility functions to handle common operations.

### 4.1 <cmath> Functions
| Function | Description |
|----------|-------------|
| std::abs(x) | Absolute value of x |
| std::max(a, b) | Return the larger of a, b |
| std::min(a, b) | Return the smaller of a, b |
| std::floor(x) | Largest integer <= x |
| std::ceil(x) | Smallest integer >= x |
| std::round(x) | Round to nearest integer (ties to even in C++11+) |
| std::sqrt(x) | Square root of x |
| std::cbrt(x) | Cube root of x |
| std::pow(a, b) | a^b |
| std::log(x) | Natural logarithm of x |
| std::log10(x) | Base 10 log of x |
| std::sin(x), etc. | Trigonometric functions |

### 4.2 Random (Modern <random>)
> Modern C++ provides robust random number generation facilities:
```cpp
#include <random>

std::random_device rd;
std::mt19937 gen(rd());
std::uniform_int_distribution<int> dist(0, 99);

int randomValue = dist(gen); // [0..99]
```

## 5. Smart Pointers & Resource Management

> Smart pointers are RAII (Resource Acquisition Is Initialization) wrappers around raw pointers that automatically manage memory allocation and deallocation.

### 5.1 std::unique_ptr (Exclusive Ownership)
> A smart pointer that owns and manages a single object, automatically deleted when the unique_ptr goes out of scope:
```cpp
#include <memory>

auto up = std::make_unique<int>(10);
std::cout << *up; // 10

auto up2 = std::move(up); // Transfer ownership to up2
```

### 5.2 std::shared_ptr (Shared Ownership)
> A reference-counting smart pointer that can be copied with multiple owners, deleting the object when the last reference is gone:
```cpp
auto sp1 = std::make_shared<int>(42);
auto sp2 = sp1;  // ref count = 2
std::cout << sp1.use_count(); // 2
```

### 5.3 std::weak_ptr (Non-owning)
> Holds a non-owning reference to an object managed by shared_ptr, helping break reference cycles:
```cpp
std::weak_ptr<int> wp = sp1;
if (auto locked = wp.lock()) {
    std::cout << *locked;
}
```

## 6. STL Containers

> The Standard Template Library (STL) provides a rich set of container classes for storing and organizing data.

### 6.1 Overview & Typical Complexity
> Understanding container performance characteristics is crucial for efficient algorithm design:

| Container | Insert (End) | Insert (Middle) | Erase (End) | Erase (Middle) | Lookup by Index | Search by Value | Underlying Structure |
|-----------|--------------|-----------------|-------------|----------------|-----------------|-----------------|----------------------|
| std::vector | Amortized O(1) | O(n) | O(1) | O(n) | O(1) | O(n) | Dynamic array |
| std::deque | Amortized O(1) | O(n) | O(1) | O(n) | O(1) | O(n) | Double-ended array blocks |
| std::list | O(1) | O(1)* w/ iterator | O(1) | O(1)* w/ iterator | N/A | O(n) | Doubly linked list |
| std::forward_list | O(1) front | O(1)* (need prev) | N/A | O(1)* (need prev) | N/A | O(n) | Singly linked list |
| std::set | O(log n) | – | O(log n) | – | N/A | O(log n) (by key) | Balanced BST (red-black tree) |
| std::unordered_set | Avg O(1) | – | Avg O(1) | – | N/A | Avg O(1) | Hash Table |
| std::map | O(log n) | – | O(log n) | – | N/A | O(log n) (by key) | Balanced BST (red-black tree) |
| std::unordered_map | Avg O(1) | – | Avg O(1) | – | N/A | Avg O(1) | Hash Table |

("Middle" insertion for lists/deques is O(1) only if you already have the correct iterator.)

### 6.2 Vector
> Dynamic array with fast random access and efficient insertion/deletion at the end:
```cpp
std::vector<int> v;
v.push_back(10);
v.pop_back();
v.size();
v.empty();
v[0];         // operator[] (no bounds check)
v.at(0);      // throws std::out_of_range
v.insert(v.begin()+i, value);
v.erase(v.begin()+i);
v.clear();
```

### 6.3 List
> Doubly-linked list with efficient insertion/deletion anywhere but no random access:
```cpp
std::list<int> lst;
lst.push_back(10);  // add end
lst.push_front(5);  // add front
lst.pop_back();
lst.pop_front();
lst.insert(it, val);
lst.erase(it);
```

### 6.4 Deque
> Double-ended queue with fast random access and efficient insertion/deletion at both ends:
```cpp
std::deque<int> dq;
dq.push_back(1);
dq.push_front(2);
dq.pop_back();
dq.pop_front();
dq[3];  // random access is O(1) typically
```

### 6.5 Set & Unordered Set
> Containers for unique elements - set (ordered using tree) and unordered_set (using hash table):
```cpp
std::set<int> s;
s.insert(10);
s.erase(10);
if (s.count(10)) { /* found */ }

std::unordered_set<int> us;
us.insert(10);
us.erase(10);
```

### 6.6 Map & Unordered Map
> Key-value associative containers - map (ordered using tree) and unordered_map (using hash table):
```cpp
std::map<int, std::string> m;
m[1] = "one";
m.insert({2, "two"});
auto it = m.find(2);
if (it != m.end()) {
    std::cout << it->second;
}

std::unordered_map<int, std::string> um;
um[1] = "one";
um.insert({2, "two"});
if (um.find(2) != um.end()) { /* ... */ }
```

### 6.7 Iterators & Range-based For
> Methods to traverse container elements:
```cpp
// Range-based for
for (int x : v) { /* ... */ }

// Classic iterator
for (auto it = v.begin(); it != v.end(); ++it) {
    std::cout << *it << " ";
}
```

## 7. Queue, Priority Queue, Stack

> Container adaptors that provide specialized functionality based on underlying containers.

### 7.1 Queue (FIFO)
> First-in, first-out data structure:
```cpp
#include <queue>

std::queue<int> q;
q.push(10);    // enqueue
q.front();     // read front
q.back();      // read last
q.pop();       // dequeue from front
q.empty();
q.size();
```

### 7.2 Priority Queue (Max-Heap by Default)
> Queue where elements are ordered by priority (largest value at top by default):
```cpp
#include <queue>
std::priority_queue<int> maxPQ;
maxPQ.push(10);
maxPQ.push(5);
maxPQ.top();   // largest
maxPQ.pop();

// Min-heap version:
std::priority_queue<int, std::vector<int>, std::greater<int>> minPQ;
```

### 7.3 Stack (LIFO)
> Last-in, first-out data structure:
```cpp
#include <stack>

std::stack<int> st;
st.push(10);
st.top();
st.pop();
st.empty();
st.size();
```

## 8. Algorithms with Lambdas

> The STL provides a rich set of algorithms that operate on containers and other sequences.

Header: `<algorithm>` (and `<functional>` for standard function objects).

### 8.1 Common Functions
> Frequently used algorithms and their time complexities:

| Algorithm | Description | Time Complexity |
|-----------|-------------|-----------------|
| `std::sort(v.begin(), v.end())` | Sorts in ascending order | O(n log n) |
| `std::sort(v.begin(), v.end(), cmp)` | Sorts using a custom comparator | O(n log n) |
| `std::binary_search(v.begin(), v.end(), val)` | Checks if value exists in a sorted range | O(log n) |
| `std::find(v.begin(), v.end(), val)` | Performs a linear search for a value | O(n) |
| `std::remove(v.begin(), v.end(), val)` | "Removes" elements by shifting (use with `erase`) | O(n) |
| `std::remove_if(v.begin(), v.end(), pred)` | Removes elements that satisfy a predicate | O(n) |
| `std::accumulate(v.begin(), v.end(), initVal)` | Computes the sum (or folds a range) | O(n) |
| `std::for_each(v.begin(), v.end(), func)` | Applies a function to each element | O(n) |
| `std::reverse(v.begin(), v.end())` | Reverses elements in a range | O(n) |
| `std::unique(v.begin(), v.end())` | Removes consecutive duplicate elements | O(n) |
| `std::lower_bound(v.begin(), v.end(), val)` | Finds the first position where `val` can be inserted without violating order | O(log n) for random-access containers |

```cpp
// Example of custom sort with lambda
std::sort(v.begin(), v.end(), [](int a, int b){ return a > b; }); // descending
```

### 8.2 emplace_back vs push_back
> emplace_back constructs elements in-place, avoiding temporary objects:
```cpp
std::vector<std::pair<int,std::string>> vec;
// push_back
vec.push_back(std::make_pair(1, "one"));
// emplace_back
vec.emplace_back(2, "two"); // constructs in-place
```

## 9. Lambdas

> Lambdas are anonymous functions that can capture variables from their surrounding scope.
```cpp
// Basic lambda
auto add = [](int a, int b) {
    return a + b;
};
std::cout << add(2,3); // 5

// Capture by value
int x = 10, y = 20;
auto sumByVal = [=]() { return x + y; };

// Capture by reference
auto sumByRef = [&]() { return x + y; };

// Generic (C++14)
auto genericLambda = [](auto a, auto b) {
    return a + b;
};
```

## 10. Additional Modern C++ Features

> C++17 and beyond introduced several powerful features that can simplify code and enhance safety.

### 10.1 Optional, Variant, Any (C++17)
> Types for representing optional values, type-safe unions, and values of any type:
```cpp
#include <optional>
std::optional<int> maybeInt;
maybeInt = 42;
if (maybeInt) {
    std::cout << *maybeInt; // 42
}

#include <variant>
std::variant<int, std::string> myVar = 10;
myVar = "Hello";
std::cout << std::get<std::string>(myVar);

#include <any>
std::any a = 1;
a = std::string("Hello");
try {
    auto str = std::any_cast<std::string>(a);
    std::cout << str;
} catch (const std::bad_any_cast& e) { /* handle */ }
```

### 10.2 Concurrency (C++11 and beyond)
> C++ provides built-in support for multi-threaded programming:

#### 10.2.1 Threads
> Basic thread management:
```cpp
#include <thread>

void worker(int id) {
    // ...
}

int main() {
    std::thread t1(worker, 1);
    std::thread t2(worker, 2);
    t1.join();
    t2.join();
}
```

#### 10.2.2 Mutex & Lock Guard
> Thread synchronization primitives:
```cpp
#include <mutex>

std::mutex m;
int counter = 0;

void safe_increment() {
    std::lock_guard<std::mutex> lock(m);
    ++counter;
}
```

#### 10.2.3 Futures / Promises
> Mechanisms for asynchronous result retrieval:
```cpp
#include <future>

int compute() { return 42; }

int main() {
    auto fut = std::async(std::launch::async, compute);
    std::cout << fut.get(); // 42
}
```

### 10.3 Filesystem (C++17)
> Standard library for filesystem operations:
```cpp
#include <filesystem>
namespace fs = std::filesystem;

int main() {
    fs::path p = "testdir";
    if (!fs::exists(p)) {
        fs::create_directory(p);
    }
    for (auto& entry : fs::directory_iterator(p)) {
        std::cout << entry.path() << "\n";
    }
}
```

## 11. Move Semantics & Perfect Forwarding

> Move semantics allows efficient transfer of resources, while perfect forwarding preserves value/reference nature of arguments.

### 11.1 Move Constructor / Assignment
> Special member functions that transfer ownership instead of copying:
```cpp
class MyArray {
    int* data;
    size_t size;
public:
    MyArray(size_t n) : data(new int[n]), size(n) {}
    ~MyArray() { delete[] data; }

    // Move constructor
    MyArray(MyArray&& other) noexcept
        : data(other.data), size(other.size) {
        other.data = nullptr;
        other.size = 0;
    }

    // Move assignment
    MyArray& operator=(MyArray&& other) noexcept {
        if (this != &other) {
            delete[] data;
            data = other.data;
            size = other.size;
            other.data = nullptr;
            other.size = 0;
        }
        return *this;
    }
};
```

### 11.2 std::move
> Converts an object to an rvalue reference, enabling resource transfer:
```cpp
std::string s = "Hello";
std::vector<std::string> v;
v.push_back(std::move(s)); // s is now "moved-from"
```

### 11.3 Perfect Forwarding
> Preserves value category (lvalue/rvalue) when passing arguments through function templates:
```cpp
template <typename T, typename... Args>
std::unique_ptr<T> make_object(Args&&... args) {
    return std::make_unique<T>(std::forward<Args>(args)...);
}
```

## 12. Additional DSA-Specific Syntax

> These specialized syntax elements and techniques are particularly useful in data structure and algorithm interview contexts.

### 12.1 Pair, Tuple, and Structured Bindings
> Convenient ways to group and access multiple values:
```cpp
#include <utility>
#include <iostream>

std::pair<int, int> p = {3, 7};
// Access in older C++:
int a = p.first;
int b = p.second;

// Or use tie:
int x, y;
std::tie(x, y) = p; // x=3, y=7

// If you only need one element:
std::tie(x, std::ignore) = p; // ignores second element

// Tuples
#include <tuple>
std::tuple<int, double, std::string> t(1, 3.14, "hello");

// Access via std::get
std::cout << std::get<0>(t); // 1
std::cout << std::get<1>(t); // 3.14

// Structured binding (C++17+):
auto [i, d, s] = t;
```

### 12.2 Bitsets and Bit Manipulation
> Efficient bit-level operations, useful for bitmasks and dynamic programming:
```cpp
#include <bitset>
#include <iostream>

// bitset of size 8
std::bitset<8> bits(0b1010); // binary literal

bits[0] = 1;       // set bit 0
bits.set(3);       // set bit 3
bits.reset(1);     // reset bit 1
bits.flip();       // flip all bits
bool isSet = bits.test(2); // check if bit 2 is set

std::cout << bits << "\n"; // e.g. "1111 0101"

// C++20 bit operations
#include <bit>
unsigned int x = 0b1010;

// Count set bits
int c = std::popcount(x);    // # of '1' bits in x
// Rotate bits
auto r = std::rotl(x, 1);    // rotate left by 1
```

 unordered_set
```cpp
struct pair_hash {
    size_t operator()(const std::pair<int,int> &p) const {
        auto h1 = std::hash<int>()(p.first);
        auto h2 = std::hash<int>()(p.second);
        // Example combine: use XOR + some shifting
        return h1 ^ (h2 + 0x9e3779b97f4a7c15ULL + (h1 << 6) + (h1 >> 2));
    }
};

struct pair_eq {
    bool operator()(const std::pair<int,int> &a, const std::pair<int,int> &b) const {
        return (a.first == b.first && a.second == b.second);
    }
};

#include <unordered_map>
std::unordered_map<std::pair<int,int>, int, pair_hash, pair_eq> mp;
mp[{1,2}] = 42;
```

### 12.4 If / Switch with Initializers (C++17)
> Combines variable initialization with conditional statements:
```cpp
if (int val = compute(); val > 0) {
    // use val here
} else {
    // val is still in scope here, if needed
}

switch (auto code = getCode(); code) {
    case 1: /* ... */ break;
    case 2: /* ... */ break;
    default: /* ... */ break;
}
```

### 12.5 next_permutation / prev_permutation
> Algorithms to generate permutations in lexicographical order:
```cpp
#include <algorithm>
#include <vector>
#include <iostream>

std::vector<int> arr = {1, 2, 3};
do {
    for (int x : arr) std::cout << x << " ";
    std::cout << "\n";
} while (std::next_permutation(arr.begin(), arr.end()));
```

### 12.6 Partial Sort, Nth Element, Partition
> Efficient algorithms for specialized sorting operations:
```cpp
#include <algorithm>
#include <vector>
std::vector<int> v{4,1,6,2,5};
int k = 3;
std::partial_sort(v.begin(), v.begin() + k, v.end());
// first k elements are sorted, the rest are in an unspecified order

std::nth_element(v.begin(), v.begin() + k, v.end());
// v[k] is the nth smallest, elements before are <= v[k], after are >= v[k].

auto pivot = std::partition(v.begin(), v.end(), [](int x){
    return x % 2 == 0; // even first
});
```

## 13. Final Tips & Best Practices

> Guidelines and best practices for modern C++ programming:

| Tip | Description |
|-----|-------------|
| RAII | Resource Acquisition Is Initialization - manage resources in constructors/destructors |
| Smart Pointers | Prefer `std::unique_ptr` or `std::shared_ptr` over raw pointers for ownership |
| `auto` | Reduces verbosity, but keep types clear where it matters |
| Range-based for | Use for cleaner iteration over containers |
| Algorithm & Lambdas | Prefer using `<algorithm>` with lambdas for more expressive, functional style |
| emplace | Use `emplace_back`, `emplace` for direct in-place construction |
| Structured Bindings | Use C++17 structured bindings to unpack pairs/tuples/structs easily |
| Const Correctness | Use `const` to prevent accidental modifications |
| Modern C++ | Compile with `-std=c++17` or `-std=c++20` to access modern features |

## 14. Common Time and Space Complexity

| Operation | Typical Time Complexity | Typical Space Complexity |
|-----------|-------------------------|--------------------------|
| Vector access | O(1) | - |
| Vector insertion (end) | O(1) amortized | - |
| Vector insertion (middle) | O(n) | - |
| HashMap/Set lookup | O(1) average | - |
| TreeMap/Set lookup | O(log n) | - |
| Quicksort / std::sort | O(n log n) | O(log n) |
| Mergesort | O(n log n) | O(n) |
| Binary search | O(log n) | O(1) |
| DFS/BFS (graph) | O(V + E) | O(V) |
| Dijkstra's algorithm | O((V + E) log V) | O(V) |

## 15. Common Interview-Specific Operations

### 15.1 String Operations

```cpp
// String to integer conversion
int num = std::stoi("123");       // 123
long long bigNum = std::stoll("9876543210");

// Integer to string conversion
std::string s = std::to_string(42);  // "42"

// Trim leading/trailing whitespace
auto trim = [](std::string s) {
    s.erase(0, s.find_first_not_of(" \t\n\r\f\v"));
    s.erase(s.find_last_not_of(" \t\n\r\f\v") + 1);
    return s;
};

// Split string by delimiter
auto split = [](const std::string& s, char delimiter) {
    std::vector<std::string> tokens;
    std::string token;
    std::istringstream tokenStream(s);
    while (std::getline(tokenStream, token, delimiter)) {
        tokens.push_back(token);
    }
    return tokens;
};
```

### 15.2 Bitwise Operations

```cpp
// Check if ith bit is set
bool isBitSet(int num, int i) {
    return (num & (1 << i)) != 0;
}

// Set ith bit
int setBit(int num, int i) {
    return num | (1 << i);
}

// Clear ith bit
int clearBit(int num, int i) {
    return num & ~(1 << i);
}

// Toggle ith bit
int toggleBit(int num, int i) {
    return num ^ (1 << i);
}

// Count set bits
int countSetBits(int num) {
    int count = 0;
    while (num) {
        count += num & 1;
        num >>= 1;
    }
    return count;
    // C++20: return std::popcount(num);
}
```

### 15.3 Graph Representation

```cpp
// Adjacency List
std::vector<std::vector<int>> graph(n);  // n nodes
graph[0].push_back(1);  // edge from 0 to 1
graph[1].push_back(2);  // edge from 1 to 2

// Weighted Graph
std::vector<std::vector<std::pair<int, int>>> weightedGraph(n);
weightedGraph[0].push_back({1, 5});  // edge from 0 to 1 with weight 5

// Adjacency Matrix
std::vector<std::vector<bool>> adjMatrix(n, std::vector<bool>(n, false));
adjMatrix[0][1] = true;  // edge from 0 to 1
```

### 15.4 Common Algorithms (Pseudocode-like C++)

#### DFS (Recursive)
```cpp
void dfs(int node, std::vector<std::vector<int>>& graph, std::vector<bool>& visited) {
    visited[node] = true;
    // Process node
    for (int neighbor : graph[node]) {
        if (!visited[neighbor]) {
            dfs(neighbor, graph, visited);
        }
    }
}
```

#### BFS
```cpp
void bfs(int start, std::vector<std::vector<int>>& graph) {
    std::vector<bool> visited(graph.size(), false);
    std::queue<int> q;
    
    visited[start] = true;
    q.push(start);
    
    while (!q.empty()) {
        int node = q.front();
        q.pop();
        
        // Process node
        
        for (int neighbor : graph[node]) {
            if (!visited[neighbor]) {
                visited[neighbor] = true;
                q.push(neighbor);
            }
        }
    }
}
```

#### Dijkstra's Algorithm
```cpp
void dijkstra(int start, std::vector<std::vector<std::pair<int, int>>>& graph) {
    int n = graph.size();
    std::vector<int> dist(n, INT_MAX);
    dist[start] = 0;
    
    std::priority_queue<std::pair<int, int>, std::vector<std::pair<int, int>>, 
                        std::greater<std::pair<int, int>>> pq;
    pq.push({0, start});  // {distance, node}
    
    while (!pq.empty()) {
        int d = pq.top().first;
        int node = pq.top().second;
        pq.pop();
        
        if (d > dist[node]) continue;
        
        for (auto& [neighbor, weight] : graph[node]) {
            if (dist[node] + weight < dist[neighbor]) {
                dist[neighbor] = dist[node] + weight;
                pq.push({dist[neighbor], neighbor});
            }
        }
    }
}
```

## 16. STL Container Modifiers and Properties

| Container | Common Operations | Notes |
|-----------|-------------------|-------|
| `std::vector<T>` | `.push_back()`, `.pop_back()`, `.resize()` | Dynamic array, contiguous memory |
| `std::list<T>` | `.push_back()`, `.push_front()`, `.splice()` | Doubly-linked list |
| `std::deque<T>` | `.push_back()`, `.push_front()`, `.pop_back()`, `.pop_front()` | Double-ended queue |
| `std::set<T>` | `.insert()`, `.erase()`, `.count()`, `.lower_bound()` | Ordered unique elements |
| `std::map<K,V>` | `[key]`, `.find()`, `.count()`, `.lower_bound()` | Ordered key-value pairs |
| `std::unordered_set<T>` | `.insert()`, `.erase()`, `.count()` | Hash table for unique elements |
| `std::unordered_map<K,V>` | `[key]`, `.find()`, `.count()` | Hash table for key-value pairs |
| `std::stack<T>` | `.push()`, `.pop()`, `.top()` | LIFO adapter |
| `std::queue<T>` | `.push()`, `.pop()`, `.front()`, `.back()` | FIFO adapter |
| `std::priority_queue<T>` | `.push()`, `.pop()`, `.top()` | Heap-based priority queue |

Typical Execution Speed: C++ solutions often handle ~10^8 operations/second in competitive programming.
