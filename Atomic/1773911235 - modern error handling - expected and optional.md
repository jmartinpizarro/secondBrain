---
aliases:
  - modern error handling - expected and optional
tags:
"References":
cssclasses:
---
# modern error handling - expected and optional

## monadic `optional`

From the *beman* library. Adds 3 template functions to optional
- `and_then` 
- `or_else`
- `transform`

```cpp
// this is going to work!
std::optional<string> opt_string("10");
std::optional<int> i = opt_string
							.and_then(std::stoi)
							.transform([](auto i){ return i * 2; });
// this is going to fail!
std::optional<string> opt_bad_string("abcd");
std::optional<int> j = opt_bad_string
							.and_then(std::stoi)
							.transform([](auto j){ return j * 2; });
```

## `expected<Return, Error>`

An error handling type similar to `optional`. Variant of a custom error type and return value, which provides support for **void returns**. For *monadic chaining functions*.

```cpp
// type definition i guess
using time_expected = std::expected<boost::posix_time::ptime, std::string>;

// time is going to be a string 'YYYYMMDDTimeDigits'

time_expected from_iso_str {std::string time} {
	try {
		ptime t = boost::posix_time::from_iso_string( time );
		return t;
	}
	catch( std::exception& e ) {
		return std::unexpected( e.what() );
	}
}

time_expected previous_day(boost::posix_time::ptime t) {
	return t - boost::gregorian::days(1);
}


int main() {
	std::string ts ( "20210726T000000" );
	auto res = from_iso_str ( ts ) ;
	
	if ( res ) {
		std::cout << to_iso_extended_string( res.value() ) << endl;
	}
	
	std::string bad_ts ( "F0210726T000000" );
	auto bad_res = from_iso_str ( bad_ts ) ;
	
	if ( !bad_res ) {
		std::cout << bad_res.error() << endl;
	}
	
	auto d = from_iso_str ( ts ).and_then( previous_day ) ;
	return 0;
}

```

### exceptions versus expected advice

- Use `expected` if calle code likely needs to handle:
	- expected isn't free
	- demands more immediate code
- Use exceptions:
	- if handler likely far away (for example a memory allocation error)
- **Can be used together**

>[!DANGER]
>What are you going to do when shit happens? If its going to be something really rare; then use an exception. Otherwise, you can use `expected`.


	

