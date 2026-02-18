# Variables

## What is Variable
A variable is a named storage location that holds a value.
Its lifetime decides how long it exists, and its scope decides where it can be accessed.
[Name → place → data, Existence = lifetime, access = scope]

## Core Properties of a Variable
    - type: Type specifies what kind of value can be stored, how much memory is reserved, and what operations are valid. [1. Memory size 2. Type of value 3. Valid Operations]
    - scope of variable: defines where the variable can be accessed. [Access] 
    - lifetime: Lifetime defines how long the variable remains in memory from creation to destruction. [Where & How declared]
    - mutablity: defines whether the value can change after initialization.
    - linkage / ownership: Linkage describes whether the variable is shared across different parts of the program or limited to a single file or scope (mostly relevant in C/C++).

## Categories of Variables
    - Local Variable: Declared inside a function or block and accessible only within that block. Created when execution enters the block. Destroyed when execution leaves the block.
    - Instance Variable: Belongs to an object. Each object has its own copy. Declared inside a class but outside methods. Created when the object is created. Destroyed when the object is destroyed.
    - Static / class Variable: Belongs to the class, not to objects. Only one copy exists and is shared. Created when the program (or class) is loaded. Destroyed when the program ends (or class is unloaded).
    - Global Variable (mainly C++): Declared outside all functions or classes. Accessible from multiple parts of the program (subject to visibility rules). Created before main starts. Destroyed when the program ends.
 
 ## Mutability
- Mutable variable: value can change.
- Constant / Final variable: value cannot change after initialization.

## Language Implementations

### C++
- Global variables can be declared outside all functions and may be accessed from different parts of the program depending on visibility rules.
- Local variables are not automatically initialized. Using them without assigning a value leads to indeterminate (garbage) data.
- Global and static variables are default-initialized.

### Java
- Java does not support true global variables. Class-level static variables are used instead.
- Local variables must be explicitly initialized before use.
- Instance and static variables receive default values if not assigned.

## Memory, Declaration & Initialization
- Declaring a variable reserves memory according to its type and storage rules.
- Initialization assigns the first value to that memory.
- If no value is provided, the result depends on the language and the kind of variable (some receive defaults, some remain uninitialized).
- A variable remains valid only during its lifetime. After that period, the memory is no longer accessible.
- If the variable is declared as constant/final, its value cannot be changed after initialization.

## Declaration Syntax Examples

### C++
#### Declaration:
    datatype variable_name;

#### Initialization:
    datatype variable_name = value;

#### Multiple variables:
    datatype a, b, c;

#### Constant:
    const datatype variable_name = value;

### Java
#### Declaration:
    datatype variable_name;

#### Initialization:
    datatype variable_name = value;

#### Multiple variables:
    datatype a, b, c;

#### Constant:
    final datatype variable_name = value;

## Examples by category

### C++
#### Local 
    int main(){
        int x=10; // accessed only inside this block
    }

#### Instance
    class Person{
    public:
        int x=10; // each object gets its own copy
    };

#### Static 
    class Person{
    public:
        static int x; // single shared copy for all objects
    };

#### Global
    int x=10; // visible globally (subject to linkage rules)
    int main(){
        // code
    }

#### LocalvsInstance
    class Val{
        int x=10;
        void LocalvsInstance(){
            int x=5;
            cout<<x; //local
            cout<<this->x; //instance
        }
    };

#### InstancevsStatic
Instance → object
Static → class
    class Person{
    public:
        int x = 1;
        static int y;
    };
    int Person::y = 0;

    int main(){
        Person p1, p2;

        p1.x = 5;
        p2.x = 7;   // different copies

        Person::y = 100; // shared
    }

### Java
#### Local
    public static void main(String[] args){
        int x=10; // accessed only this block
    }

#### Instance
    class Person{
        int x=10;
    }

#### Static 
    class Person{
        static int x;
    }

#### LocalvsInstance
    class Val{
        int x=10;
        void LocalvsInstance(){
            int x=5;
            System.out.println(x); //local
            System.out.println(this.x); //instance
        }
    }
#### InstancevsStatic
    class Person{
    int x = 1;
    static int y;
    }
    class Main{
        public staitc void main(String[] args){
            Person p1 = new Person();
            Person p2 = new Person();
            p1.x=5;
            p2.x=7; // different copies

            Person.y = 100; //shared
        }
    }

## Initialization behavior

- In C++, local variables are uninitialized by default. Global and static variables are zero-initialized.
- in java, local must be initialized, instance and static will get a default value 

## Memory Area Hint (Conceptual Model)

This is a simplified conceptual model used for understanding.
Actual memory layout and optimizations may vary by compiler/JVM.

- Local variables → typically associated with stack frames.
- Instance variables → live inside objects, typically on the heap.
- Static / global variables → stored in static storage and exist for the program lifetime.

## Value vs Reference

- Primitive variables store the actual value.
- Reference variables store the address of an object.
- In Java, objects are accessed through references.
- In C++, objects can be accessed directly or via pointers/references.

## Parameter Passing

    - Pass by value: a copy of the variable is passed.
    - Pass by reference: the original variable is accessed.
In Java, everything is pass-by-value. When objects are passed, the reference is copied.

## Compile-Time vs Runtime Variables

- Static/global variables are allocated before program execution.
- Local variables are created at runtime when function executes.
- Dynamically allocated memory (new / malloc) exists until manually freed or garbage collected.

## Variable Shadowing

When a local variable has the same name as an instance or global variable, the local variable hides it within its scope.

## Quick Recall Map

Variable = Name + Type + Memory + Lifetime + Scope + Mutability

Local → block lifetime → must initialize (Java)
Instance → object lifetime → default initialized
Static → class/program lifetime → single shared copy
Global (C++) → program lifetime

Primitive → stores value
Reference → stores address/reference

Initialization rules differ by language.
