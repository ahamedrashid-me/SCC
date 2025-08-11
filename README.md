SuperCode Programming Language

Welcome to SuperCode, a statically-typed programming language built for performance and memory safety. It combines a modern, ergonomic syntax with powerful features like a Rust-inspired ownership model and compile-time constants. The language is designed to help developers write robust, high-performance applications with confidence.
Key Features
💻 Syntax and Structure

SuperCode programs are organized into modules and have a single entry point: the run block. It uses square brackets [] for function calls, providing a distinct and clean syntax.

    Ergonomic Syntax: Square brackets [] for function calls and the -> operator for structs.

    Program Structure: Organized into modules, with a main entry point in the run block.

    Comments: Supports both single-line (//) and multi-line (/? ?/) comments.

🧠 Data and Types

SuperCode is statically-typed and offers a rich set of built-in types. This design ensures that type-related errors are caught at compile time.

    Simple Types: Includes num, deci, text, char, bool, and low-level types like byte and ubyte.

    Null Safety: Types are non-nullable by default. Optional data is handled with nullable types, denoted by a question mark (?).

    Immutability: The val keyword creates true compile-time constants, ensuring zero-runtime-overhead immutable values.

    Advanced Types: Supports user-defined composite types with struct and type-safe enums with enum.

⚙️ Control Flow and Error Handling

The language provides a set of powerful and readable control flow structures, simplifying complex logic.

    Conditional Logic: The if-or-else structure offers a flexible way to handle branching, with or blocks acting as else if.

    Pattern Matching: The repeat-when-fixed structure provides a type-safe alternative to traditional switch-case statements.

    Looping: It has both a C-style for loop and a convenient for-each loop for iterating over collections.

    Robust Error Handling: The try-catch-finally block allows for safe handling of runtime exceptions, with a dedicated block that always executes for cleanup.

🛡️ Memory Safety

A core feature of SuperCode is its Rust-inspired memory model, which prevents common memory-related bugs at compile time.

    Ownership Model: The take, give, and free keywords provide explicit control over memory, ensuring that every piece of data has a single, clear owner.

    Automatic Deallocation: The compiler tracks ownership to automatically manage memory and prevent common issues like dangling pointers and double-frees.

Getting Started
Installation

SuperCode is currently under development. The SuperCode compiler, which translates .su files into native binaries, is available for download on the releases page.

# Example: Download the compiler and add to your PATH
wget https://github.com/your-repo/supercode/releases/download/v0.1/sc_compiler-v0.1.zip
unzip sc_compiler-v0.1.zip
export PATH=$PATH:$(pwd)/sc_compiler


Writing Your First Program

Create a file named hello.su with the following code. For more examples, see the ../examples/ directory.

// Define a function that returns a num
fnc add_numbers[num a, num b]:num {
    return a + b;
}

// Main program entry point
run {
    val num FIVE = 5;
    num my_result = @add_numbers[5, 10];
    @print["The result is: ${my_result}"];
};


Compilation and Execution

To compile and run your SuperCode program, use the sc compiler from your terminal.

# Compile the file or see help scc
scc hello.su   

# Run the compiled binary
./hello
# Output: The result is: 15


Documentation

This repository contains comprehensive documentation to help you learn SuperCode:

    Complete Language Reference: A detailed guide to all language features.

    Getting Started Guide: Step-by-step instructions for beginners.

    Compiler Guide: Technical details on compiler usage.

Roadmap & Future Plans

The next major areas of focus for the SuperCode project are:

    Expanding the Standard Library: Building out more modules for common tasks like file I/O and networking.

    Improving Error Messages: Enhancing the compiler to provide more specific, actionable feedback.

    Implementing a Package Manager: Creating a system to easily manage and share SuperCode libraries.

Contributing

We welcome contributions! Please feel free to open issues or submit pull requests.
License

This project is licensed under the MIT License - see the LICENSE file for details.








# SCC
this is a compiler for SuperCode Programming Languages.

<img width="1144" height="1428" alt="image" src="https://github.com/user-attachments/assets/b8146670-41e3-4492-a4d1-7aa0288d45f2" />

### supm - supercode package manager

<img width="1354" height="1348" alt="image" src="https://github.com/user-attachments/assets/465f3e30-274d-41a7-a233-2f5f5fcdf2aa" />
