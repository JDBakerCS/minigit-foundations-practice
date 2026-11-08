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


## Exercise 4 Fill in the blanks

Complete the missing lines so the function creates missing folders, writes the text, and reports failure.

```cpp
bool save(const std::filesystem::path& file, const std::string& text) {
    if (!file.parent_path().empty()) {                       // (1) only if there is a parent folder
        std::filesystem::create_directories(file.parent_path());   // (2) make all missing folders
    }
    std::ofstream output(file);
    if (!output) {                                       // (3) did opening fail?
        return false;
    }
    output << text;
    return static_cast<bool>(output);                              // (4) true only if writing worked
}
```

---
