HW9 Practice Answers

## Exercise 1: Predictions

a: prints the path to the HEAD file as a string

b: error

c: only reads the filename notes.txt

d: returns docs

e: checks whether the parent path is empty not whether the file exists.

f: returns the first extension including the dot

ex1_paths.cpp ran:

a: repo/.minigit/HEAD
b: /HEAD
c: notes.txt
d: docs
e: 1
f: .txt

## Exercise 2

`getline` removes the newline from each line, so joining the lines gives ab. Reading the whole stream with rdbuf() keeps the newlines example:

```C++
#include <fstream>
#include <sstream>

std::string readAll(const std::filesystem::path& file) {
    std::ifstream input(file);
    std::ostringstream contents;
    contents << input.rdbuf();
    return contents.str();
}
```


## Exercise 3

Fixed:

```C++
std::filesystem::path metadataDirectory(const std::filesystem::path& root) {
    return root / ".minigit";
}
std::filesystem::path headFile(const std::filesystem::path& root) {
    return metadataDirectory(root) / "HEAD";
}
```
