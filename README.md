# wrap_python_cpp_example
Example of compiling C++ shared library (.so file) and wrapping with Python.  
In this example we use `g++` and `python3` on a Unix system.

## Step 1 - Compiling C++
Generate a file `file.cpp` containing the following:
```cpp
#include <iostream>
using namespace std;

extern "C" // makes C++ functions accessible
{

int my_function(int arg){
	cout<<"In C++ my_function. You passed me: "<<arg<<endl;
	return arg*2;
}

} // end extern "C"

```
Compile object file (.o) from .cpp file
```bash
g++ -c -Wall -Werror -fPIC file.cpp -o file.o
```
Generate shared library file (.so)
```bash
g++ file.o -shared -o libfile.so
```
Your directory structure should now look like:
```bash
└── my_folder/
    ├── file.cpp
    ├── file.o
    └── libfile.so
```
## Step 2 - Wrapping with Python
Generate a file `file.py` containing the following:
```python
import ctypes

# load shared library file
c_lib = ctypes.CDLL("./libfile.so")
# now we can access the functions defined within `extern "C"{}`
a = c_lib.my_function(21)
print("a = {}".format(a))

```
Your directory structure should now look like:
```bash
└── my_folder/
    ├── file.cpp
    ├── file.o
    └── file.py
    └── libfile.so
    
```
Execute the Python file
```bash
python file.py
```
output:
```bash
In C++ my_function. You passed me: 21
a = 42

```
