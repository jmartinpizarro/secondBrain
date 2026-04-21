---
aliases:
  - string processing
tags:
"References":
cssclasses:
---
# string processing

---

`basic_string::contains`
`starts_with` and `ends_with` got added in C++20.

---

`string` and nullptr
It is possible to assign a *nullptr* to a string variable. Just harder! -> Generates an error.
*The note maker does not understand why somebody will do this. Fuck me.*

```cpp
std::string doIt() {
	return nullptr;
}

int main(){
	std::string string_ptr = doIt();
	print("{}\n", string_ptr);
}
```

---

`resize_and_overwrite`
Performance for strings. Not really that useful unless you are using the same string thousands of times.

---

`range` constructor for `string_view`

---



