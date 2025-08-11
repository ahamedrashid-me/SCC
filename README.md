SuperCode v0.1 

Welcome to SuperCode, a statically-typed programming language built for performance and memory safety. It combines a modern, ergonomic syntax with powerful features like a Rust-inspired ownership model and compile-time constants. SuperCode's core philosophy is to empower developers to write robust, high-performance applications with confidence, preventing an entire class of common errors at compile time rather than runtime.
Key Features
💻 Syntax and Structure

SuperCode programs are organized into modules and have a single entry point: the run block. This structure provides a clean, predictable foundation for projects of any size. It uses square brackets [] for function calls, a deliberate design choice that visually separates function invocations from array access or other syntactic elements.

    Ergonomic Syntax: The use of square brackets [] for function calls offers a distinct and clean syntax. Similarly, the -> operator for accessing struct members provides a clear, C-style visual cue for dereferencing a composite data type.

    Program Structure: Organized into modules, which define the scope for all code within a file and prevent naming conflicts. The run block serves as the main entry point, ensuring a predictable and well-defined start to every program's execution.

    Comments: Supports both single-line (//) and multi-line (/? ?/) comments, allowing for clear and effective documentation directly within the code.

🧠 Data and Types

SuperCode is statically-typed and offers a rich set of built-in types. This design ensures that type-related errors are caught at compile time, leading to more reliable and predictable applications. In addition to standard types, it provides fine-grained control for low-level tasks and a powerful system for complex data modeling.

    Simple Types: Includes a full suite of standard types such as num (a 32-bit integer), deci (a 64-bit double-precision float), text, char, and bool. For performance-critical or embedded systems programming, it also offers low-level integer types like byte and ubyte.

    Null Safety: Types are non-nullable by default, a core design principle to prevent unexpected null-pointer errors, one of the most common sources of application crashes. Optional data is handled with nullable types, denoted by a question mark (?), which forces developers to handle the null case explicitly, guaranteeing safety and reliability.

    Immutability: The val keyword creates true compile-time constants. Expressions like arithmetic and string interpolation are evaluated at compile time, completely eliminating runtime overhead. This is ideal for defining configuration settings, mathematical constants, or other values that should never change. For example, val num CALC_RESULT = (20 + 5) * 2; is computed by the compiler to the value 50.

    Advanced Types: The struct keyword allows you to create user-defined composite data types for grouping related data, such as a Point with num x and num y fields. Type-safe enums with enum provide a clean way to define a finite set of named constants, making code more readable and preventing invalid values.

⚙️ Control Flow and Error Handling

The language provides a set of powerful and readable control flow structures, simplifying complex logic and making code easier to maintain and reason about.

    Conditional Logic: The if-or-else structure offers a flexible way to handle branching, with or blocks acting as else if. This concise syntax allows for clear, multi-level conditional logic without the "pyramid of doom" that can occur with deeply nested if statements in other languages.

    Pattern Matching: The repeat-when-fixed structure provides a type-safe and highly readable alternative to traditional switch-case statements. It's especially useful for implementing state machines, command handlers, or parsing different data types by matching against a value and executing a corresponding code block. The quit; keyword provides explicit control over when the match block should terminate.

    Looping: SuperCode has both a classic C-style for loop and a convenient for-each loop for iterating over collections, providing flexibility for different iteration needs.

    Robust Error Handling: The try-catch-finally block allows for safe handling of runtime exceptions, such as file I/O or network failures. The dedicated finally block ensures that critical cleanup operations, like closing a file handle or releasing a network connection, always execute, regardless of whether an error occurred.

🛡️ Memory Safety

A core feature of SuperCode is its Rust-inspired memory model, which prevents common memory-related bugs at compile time. This is achieved by tracking the ownership of data, making it impossible to create dangerous situations like dangling pointers or data races.

    Ownership Model: The take and give keywords provide explicit control over memory. take moves ownership of data from one variable to another, ensuring that the original variable can no longer be used. give creates a temporary reference, allowing a function to use the data without taking ownership, similar to a temporary "lease" on the resource.

    Automatic Deallocation: The compiler tracks ownership to automatically manage memory and prevent common issues like dangling pointers and double-frees. When a variable goes out of scope, the compiler automatically deallocates its memory, making the free keyword necessary only for specific, advanced cases where manual deallocation is required.

Getting Started
Installation

SuperCode is currently under development. The SuperCode compiler, which translates .su files into native binaries, is available for download on the releases page.

# Example: Download the compiler and add to your PATH
wget [https://github.com/ahamedrashid-me/SCC/releases/tag/releasv0.01]

unzip 

export PATH=$PATH:$(pwd)/scc supm 

or sudo chmod 777 scc supm
mv sccsupm /bin

Writing Your First Program

Create a file named hello.su with the following code. This simple program demonstrates the core syntax and structure of SuperCode. For more examples, see the ../examples/ directory.

// Define a function that adds two numbers and returns the sum
fnc add_numbers[num a, num b]:num {
    return a + b;
}

// Main program entry point, where execution begins
run {
    // Define a compile-time constant using the 'val' keyword
    val num FIVE = 5;
    
    // Call the function and store the result in a new variable
    num my_result = @add_numbers[5, 10];
    
    // Use advanced string interpolation to print the result to the console
    @print["The result is: ${my_result}"];
};

Compilation and Execution

To compile and run your SuperCode program, use the sc compiler from your terminal. The compiler will produce a native executable file.

# Compile the file using the 'sc compile' command
scs compile hello.su   

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

    

Contributing

We welcome contributions! Please feel free to open issues or submit pull requests.
License

This project is licensed under the MIT License 


<img width="1144" height="1428" alt="image" src="https://github.com/user-attachments/assets/b8146670-41e3-4492-a4d1-7aa0288d45f2" />


<img width="1354" height="1348" alt="image" src="https://github.com/user-attachments/assets/465f3e30-274d-41a7-a233-2f5f5fcdf2aa" />
