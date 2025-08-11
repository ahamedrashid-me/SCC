SuperCode v0.1 Complete Language Reference

This document provides a comprehensive and expanded reference for the SuperCode programming language, detailing its syntax, core features, and practical use cases.
1. Core Language Features

This section covers the foundational elements of a SuperCode program.
1.1 Program Structure: Modules and run

Every SuperCode program is organized into modules and has a single entry point: the run block.

Feature:

    module: Defines the scope for code.

    run: The main function where execution begins.

Use Case:
Essential for creating any executable program, from simple scripts to large applications.

module main;

run {
  @print["Program execution starts here."];
}


1.2 Statements and Comments

All statements must end with a semicolon. SuperCode supports standard single-line and multi-line comments.

Features:

    Semicolon: Terminates all statements.

    //: Single-line comment.

    /? ... ?/: Multi-line comment.

Use Case:
Improves code readability and allows for internal documentation.

// A single-line comment explaining the variable's purpose.
var my_var = 50;

/?
This is a block comment
that can span multiple lines.
It describes the following `run` block.
?/

run {
  @print["A statement must end with a semicolon."];
}


2. Variables, Constants, and Data
2.1 Basic Data Types

SuperCode is statically typed and includes a robust set of basic data types.

Features:

    num: Signed 32-bit integer.

    deci: 64-bit double-precision floating-point.

    text: String type.

    char: Single character.

    bool: Boolean (true or false).

    byte: Signed 8-bit integer.

    ubyte: Unsigned 8-bit integer.

Use Case:
Declaring variables with specific types for performance and safety.

var name = "Alice";    // Type inferred as text
num age = 25;          // Explicit type declaration
deci pi = 3.14159;
bool is_online = true;
byte level = 10;


2.2 Nullable Types

Any data type can be made nullable by appending a question mark ?, ensuring null safety.

Features:

    type?: Declares a type that can hold null.

Use Case:
Handling optional data, such as a user's middle name or a function's return value that might not exist.

text? middle_name = null;

if [middle_name != null] {
  @print["Middle name: ${middle_name}"];
} else {
  @print["No middle name provided."];
}


2.3 Compile-Time Constants (val)

The val keyword creates genuine compile-time constants with zero runtime overhead.

Features:

    val: Declares a constant that must be initialized with a compile-time value.

    Constant Folding: Arithmetic expressions and string interpolations are evaluated at compile time.

Use Case:
Defining immutable values like configuration settings, API keys, or mathematical constants.

val num MAX_USERS = 100;
val num CALC_RESULT = (20 + 5) * 2; // This is computed at compile time (50)

run {
  @print["The maximum number of users is ${MAX_USERS}."];
  @print["The pre-calculated result is ${CALC_RESULT}."];
}


2.4 Advanced String Interpolation

SuperCode uses advanced interpolation with ${...} to embed variables and expressions directly within strings.

Features:

    ${...}: Embeds a variable or an expression inside a string literal.

Use Case:
Creating dynamic and readable output strings without explicit concatenation.

var item_name = "Laptop";
var price = 1200;
var tax_rate = 0.08;

run {
  @print["Item: ${item_name}, Price: $${price}"];
  @print["Total cost including tax: $${price * (1 + tax_rate)}"];
}


3. Functions and Operations
3.1 Function Definition and Calls

Functions are declared with fnc, and function calls use an @ prefix with square brackets.

Features:

    fnc: Keyword for defining a function.

    @function_name[]: Syntax for calling a function.

    return: Specifies the function's return value.

Use Case:
Encapsulating reusable logic to organize code.

fnc add_numbers[num a, num b]:num {
  return a + b;
}

run {
  num result = @add_numbers[10, 20];
  @print["The sum is ${result}."];
}


3.2 Operators

SuperCode supports a wide range of operators.

Features:

    Arithmetic: +, -, *, /, %

    Comparison: ==, !=, <, >, <=, >=

    Logical: && (AND), || (OR), ! (NOT)

    Compound Assignment: +=, -=, *=, /=, %=

    Ternary: (condition) ? value_if_true : value_if_false

Use Case:
Performing calculations, making comparisons, and controlling logic.

run {
  var x = 10;
  var y = 3;
  
  // Compound assignment and logical operators
  x += 5; // x is now 15
  bool is_valid = (x > y) && (x % 2 == 1);
  @print["Is valid: ${is_valid}"];
  
  // Ternary operator
  text message = (is_valid) ? "The condition is true." : "The condition is false.";
  @print[message];
}


4. Control Flow and Error Handling
4.1 Conditional Logic (if-or-else)

The if-or-else structure handles branching logic with an optional or block, functioning as an else if.

Feature:

    if[condition] { ... }: The initial conditional block.

    or[condition] { ... }: The else if block.

    else { ... }: The optional fallback block.

Use Case:
Handling different scenarios based on conditions, such as checking user roles or validating input.

fnc check_status[num code]:void {
  if[code == 200] {
    @print["Status: OK"];
  }or[code == 404] {
    @print["Status: Not Found"];
  }else{
    @print["Status: Unknown"];
  }
}

run {
  @check_status[200];
  @check_status[404];
  @check_status[500];
}


4.2 Looping (for and for-each)

SuperCode provides two types of loops for iteration.

Features:

    for[]: A C-style loop with an initializer, condition, and incrementor.

    for[item in collection]: An easy-to-use loop for iterating over collections.

Use Case:
Repeating actions, processing lists of items, and more.

run {
  // C-style loop
  @print["Countdown:"];
  for[num i = 3; i > 0; i = i - 1] {
    @print["${i}"];
  }
  
  // For-each loop
  text[] fruits = ["Apple", "Banana", "Cherry"];
  @print["My favorite fruits:"];
  for[fruit in fruits] {
    @print["- ${fruit}"];
  }
}


4.3 Pattern Matching (repeat-when-fixed)

The repeat-when-fixed structure is a type-safe and readable alternative to nested if-or-else statements.

Features:

    repeat[value]: The value to match against.

    when value { ... }: A block that executes if the value matches.

    quit;: Exits the repeat block after a match.

    fixed { ... }: The default case.

Use Case:
Implementing state machines, command handlers, or menu-driven applications.

fnc handle_command[text command]:void {
  repeat[command] {
    when "start" {
      @print["Starting service..."];
    } quit;
    when "stop" {
      @print["Stopping service..."];
    } quit;
    fixed {
      @print["Invalid command."];
    }
  }
}

run {
  @handle_command["start"];
  @handle_command["status"];
}


4.4 Exception Handling (try-catch-finally)

The try-catch-finally block provides a robust mechanism for handling runtime errors.

Features:

    try: Contains code that might throw an exception.

    catch: Captures and handles a thrown exception.

    finally: A block that always executes, regardless of whether an exception occurred.

Use Case:
Safely handling operations that can fail, such as file I/O or network requests.

fnc divide_safely[num x, num y]:void {
  try {
    if[y == 0] {
      throw "Division by zero is not possible.";
    }
    @print["Result: ${x / y}"];
  } catch[error_msg] {
    @print["Error caught: ${error_msg}"];
  } finally {
    @print["Cleanup finished."];
  }
}

run {
  @divide_safely[10, 2];
  @divide_safely[10, 0];
}


5. Memory Management and Advanced Types
5.1 Memory Model: Ownership and Borrowing

SuperCode uses a Rust-like ownership model to prevent memory-related bugs.

Features:

    var: Declares a variable with ownership.

    take: Moves ownership of a variable. The original variable is no longer valid.

    give: Borrows a reference to a variable, allowing temporary use without transferring ownership.

    free: Explicitly deallocates a variable's memory.

Use Case:
Creating high-performance, memory-safe system-level applications.

struct Resource {
  text name;
};

fnc process_resource[give Resource r]:void {
  @print["Processing resource: ${r->name}"];
}

run {
  var my_resource = Resource{name: "Data file"};
  @process_resource[give my_resource]; // Borrow a reference
  @print["Resource still owned: ${my_resource->name}"]; // Still valid
  
  var new_owner = take my_resource; // Move ownership
  // my_resource is now invalid
  
  free new_owner; // Explicitly free memory
}


5.2 Structs and Nested Structs

Structs are user-defined composite data types for grouping related data. They can contain other structs, allowing for complex data models.

Features:

    struct: Defines a new data structure.

    ->: The member access operator.

Use Case:
Modeling real-world entities like users, products, or vectors.

struct Point {
  num x;
  num y;
};

struct Circle {
  Point center;
  num radius;
};

run {
  var my_circle = Circle{
    center: Point{x: 10, y: 20},
    radius: 5
  };
  
  @print["Circle's center is at x: ${my_circle->center->x}, y: ${my_circle->center->y}"];
}


5.3 Enums

Enums provide a type-safe way to define a set of named constants.

Feature:

    enum: Defines a new enumeration type.

Use Case:
Representing a finite set of values, such as a state machine's states or the days of the week.

enum Direction {
  NORTH,
  SOUTH,
  EAST,
  WEST
}

run {
  var current_direction = Direction.NORTH;
  if [current_direction == Direction.NORTH] {
    @print["We are moving North."];
  }
}


5.4 Collections: Arrays

SuperCode supports fixed-size and multi-dimensional arrays.

Features:

    type[size]: Fixed-size array declaration.

    .length[]: A property to get the array's length.

    type[size1][size2]: Multi-dimensional array declaration.

Use Case:
Storing collections of items, matrix calculations, and data tables.

run {
  num[5] my_array = [10, 20, 30, 40, 50];
  @print["Array length is ${my_array.length[]}"];
  @print["Third element is ${my_array[2]}"];
  
  num[2][2] matrix = [[1, 2], [3, 4]];
  @print["Matrix value at [1][0] is ${matrix[1][0]}"];
}


5.5 Collections: Sets and Maps

SuperCode provides built-in support for sets and maps.

Features:

    {item1, ...}: A set literal.

    {"key": value, ...}: A map literal.

Use Case:
Using sets for unique collections of data and maps for key-value lookups.

run {
  var my_set = {1, 2, 3, 2, 1}; // Contains {1, 2, 3}
  @print["Set contains 3 unique elements. Actual size: ${@len[my_set]}"];
  
  var user_profile = {"username": "user123", "id": 456, "is_active": true};
  @print["User profile: ${user_profile["username"]}"];
}


6. Import System and Built-in Functions
6.1 Import Mechanism

The import keyword allows a program to use code from external modules. SuperCode distinguishes between importing a standard library and a local SuperCode library.

Features:

    import stdlib.module_name;: Imports a module from the standard library.

    import /path/to/module.sulib;: Imports a local SuperCode library file.

Use Case:
Organizing large projects into separate files and reusing code from both the standard library and custom modules.

// A simple example of importing a standard math library.
import stdlib.math;

// A simple example of importing a local SuperCode library.
import "/my_libs/string_utils.sulib";

run {
  // Now we can use functions from the imported libraries
  num result = @math.power[2, 8];
  @print["2 to the power of 8 is ${result}"];
}


6.2 Standard Library Functions

SuperCode includes a variety of built-in functions for common tasks, categorized below.
General Utility Functions

These functions provide fundamental capabilities for input/output and collection management.

    @print[value]: Prints a value to the console.

    @len[collection]: Returns the length of a collection (string, array, set, or map).

    @read[prompt]: Reads a line of text from the console.

Type Conversion Functions

These functions are used to safely convert values from one type to another.

    @to_text[value]: Converts a value to a text (string).

    @to_num[value]: Converts a value to a num (integer).

    @to_deci[value]: Converts a value to a deci (float).

    @to_bool[value]: Converts a value to a bool (boolean).

String Manipulation

SuperCode's primary method for string manipulation is advanced interpolation. The ${...} syntax is used for all string concatenation and embedding of variables or expressions.

    String Slicing: You can get a substring using a slicing syntax.

        my_string[start..end]: Returns a new string containing characters from the start index (inclusive) to the end index (exclusive).

        my_string[start..]: Returns a new string from the start index to the end.

Use Case:
Performing basic I/O, converting data types, and easily building dynamic strings.

run {
  // General Utility
  text user_input = @read["Enter a number: "];
  @print["You entered: ${user_input}"];
  
  // Type Conversion
  num my_num = @to_num[user_input];
  @print["Your number plus 10 is: ${my_num + 10}"];
  
  // String Manipulation
  text sentence = "SuperCode is great.";
  text sliced_text = sentence[11..16]; // "great"
  @print["Sliced string: ${sliced_text}"];
  
  @print["Full string length: ${@len[sentence]}"];
}

