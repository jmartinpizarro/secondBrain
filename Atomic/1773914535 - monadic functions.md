---
aliases:
  - monadic functions
tags:
"References":
cssclasses:
---
# monadic functions

Functions that can be applied sequentially. And with some beautiful effects:
- `and_then` 
- `or_else`
- `transform`

```cpp
#include <vector>
#include <ranges> // for std::views::ranges
#include <print> // for std::print
#include <beman/optional/optional.hpp>

using beman::optional::optional;

int main() {

	using optint = beman::optional::optional<int>;
	std::vector<optint> numbers{{5},{},{2}, {}};
	std::print("[");
	
	for( auto iii : numbers ) {
	// rewrite the code using a monadic functions
	//if ( iii.has_value() )
	//{
	// std::print("{} ", iii.value());
	//}
	//else
	//{
	// std::print("* ");
	//}
	
	// transform solo se ejecuta si hay un valor!
	
	iii
		.transform([&](int v) {
			std::print("{} ", v);
			return v;
		})
		.or_else([&]() {
			std::print("* ");
			return optional<int>{};
		}
		);
	
	}
	
	std::println("]");
	std::println("val: {} size:{}", numbers, numbers.size() );
	return 0;
}
```

