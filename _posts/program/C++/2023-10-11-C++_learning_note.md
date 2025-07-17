---
categories: [Program lang, C++]
tag: C++
---
# 2023-10-11-C++_learning_note

快速编译方法：
- GCC
    - g++[^g] -std=c++17[^std] -W[^w] -Wall[^wall] -Wfatal-errors[^wfatal-errors] filename
    - g++:
    

[^g]: 这是GNU Compiler Collection（GNU编译器集合）的C++编译器。
[^std]: 这是编译器选项，指定了所使用的C++标准版本。在这里，-std=c++17表示编译器将使用C++17标准进行编译。
[^w]: 这是编译器选项，用于开启警告信息。
[^wall]: 这也是编译器选项，用于开启更多警告。-Wall表示开启所有警告，以便编译器能检查源代码中可能存在的潜在问题。
[^wfatal-errors]: 这也是编译器选项，用于开启更多警告。-Wall表示开启所有警告，以便编译器能检查源代码中可能存在的潜在问题。

- Clang
    - clang++ -std=c++17 -W -Wall -Wfatal-errors filename

- MSVC
    - cl /std:c++17 /EHsc[^ehsc] /W3[^w3] filename
    


[^ehsc]: 这是编译器选项，用于启用异常处理。/EHsc表示启用标准的C++异常处理。
[^w3]: 这是编译器选项，用于指定警告级别。/W3表示使用较高的警告级别，以便编译器能检查源代码中可能存在的潜在问题。