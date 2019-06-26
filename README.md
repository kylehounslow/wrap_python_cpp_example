# wrap_python_cpp_example
Example of compiling C++ shared library (.so file) and wrapping with Python

## Step 1 - Compiling C++
### Compile object file (.o) from .cpp file
```bash
g++ -c -Wall -Werror -fPIC file.cpp -o file.o
```
### Generate shared library file (.so)
```bash
g++ file.o -shared -o libfile.so
```

## Step 2 - Wrapping with Python

```bash
#TODO
```
