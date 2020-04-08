# any_ptr
A simple single-header smart pointer that wraps other kinds of smart pointers.

## Usage

```
$ git submodule add git@github.com:xloem/any_ptr
$ git submodule update --init --recursive
```

```
#include <memory>
#include <iostream>

#include "any_ptr/any_ptr"

using namespace any_ptr_ns;
using namespace std;

int main()
{
	// any_ptr can wrap 3 different kinds of pointers

	// std::unique_ptr
	any_ptr<string> smart_hello = make_unique<string>("Hello, ");

	// std::shared_ptr
	any_ptr<string> smart_world = make_shared<string>("world!");

	// and c-style bare pointers
	any_ptr<string> smart_hello_world_needscleanup = new string("Hello, world!");

	// any_ptr is usable as a pointer, like each type it wraps
	cout << *smart_hello << *smart_world << endl;
	cout << *smart_hello_world_needscleanup << endl;

	// c-style bare pointers do not automatically delete;
	// they are intended for passing pointers from memory otherwise-managed
	delete smart_hello_world_needscleanup.get();

	// c++-style smart pointers do automatically delete.
	// smart_hello and smart_world free their contents on return

	return 0;
}
```
