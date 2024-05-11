HeapMemoryAnalyzer
==========================

## Summary
Analyzer of heap memory operations for C/C++ programs. Detects: Memory Leak, Double Free. Determines the total number of the operations, and the maximum amount of heap memory used. As a result of work generates a file with analysis and accurate positions in logs where problems were detected

## Usage
Here's a simple and clear example of using HeapMemoryAnalyzer. The analysis occurs over the logs obtained during the program ranning. To generate the logs that will be analyzed in the C/C ++ program, you need to override new/malloc and delete/free operations. The following example is given for C++ program:
```c++
void* operator new(std::size_t sz) {
	void *ptr = std::malloc(sz);
	cout << endl << "[_NEW_:" << hex << ptr << dec << ":" << sz << "]" << endl;
	return ptr;
}

void* operator new[](std::size_t sz) {
	void *ptr = std::malloc(sz);
	cout << endl << "[_NEW_:" << hex << ptr << dec << ":" << sz << "]" << dec << endl;
	return ptr;
}

void operator delete(void* ptr) noexcept {
	cout << endl << "[_DELETE_:" << hex << ptr << "]" << dec << endl;
	std::free(ptr);
}

void operator delete[](void* ptr) noexcept {
	cout << endl << "[_DELETE_:" << hex << ptr << "]" <<  dec << endl;
	std::free(ptr);
}
```
Example of starting the script: 
```
python3 mem_heap_corruption_analyzer logs.txt
```

## Authors
1. VSkoshchuk (<skoschuk999@gmail.com>)

