# Variables — Foundations

### 1. Definition
A variable is a named binding between:
- A type
- A memory location
- A lifetime
- A scope
- A mutability rule
    
        A variable is **not just a box that stores data.**

It is a contract between:
- The compiler (type rules)
- The runtime (lifetime & memory behavior)
- The memory model (allocation and layout rules)

---

### 2. Core Properties (Language-Independent)

Every variable has these properties.

---

#### 2.1 Type
Defines:
- What data can be stored
- Memory size
- Valid operations
- Representation in memory

Why it matters:
- Enforces compile-time safety.
- Influences memory layout.
- Impacts performance and correctness.

---

#### 2.2 Scope
Defines where a variable is accessible.

Common scopes:
- Block scope
- Function/method scope
- Class scope
- Global scope (C++)

Scope is a compile-time property.

Scope ≠ Lifetime.

A variable may be inaccessible yet still alive.

---

#### 2.3 Lifetime
Defines how long a variable exists in memory.

Typical lifetimes:
- Block duration (local variables)
- Object lifetime (instance variables)
- Program lifetime (static/global)
- Until class unloading (Java static fields)

Lifetime is a runtime property.

---

#### 2.4 Mutability
Defines whether value can change after initialization.
- Mutable → value can change
- Immutable → `const` (C++), `final` (Java)

Immutability is a design decision.

It does not change scope or lifetime.

---

#### 2.5 Linkage (C++)
Defines visibility across translation units.
- Internal linkage
- External linkage

Linkage is resolved at link time, not runtime.

(Java does not expose linkage explicitly.)

---

### Core Property Separation

#### 1. Scope vs Lifetime
- Scope → where it can be accessed (compile-time)
- Lifetime → how long it exists (runtime)

They are independent.

#### 2. Lifetime vs Storage Location
- Lifetime is a language rule.
- Stack/heap is an implementation detail.

#### 3. Mutability vs Lifetime
- const / final does not change lifetime.
- It changes write permissions.

#### 4. Linkage vs Scope (C++)
- Scope → visibility in source code
- Linkage → visibility across translation units

---
### 3. Categories of Variables
---

#### 3.1 Local Variable
- Declared inside function or block
- Scope = block
- Lifetime = block execution
- Automatic storage duration (C++). 
- Typically implemented using stack frames, but not guaranteed by the standard.

##### C++:
- Not automatically initialized
- Using uninitialized locals → undefined behavior

##### Java:
- Must be explicitly initialized before use

---

#### 3.2 Instance Variable
- Declared inside class
- Belongs to object
- One copy per object
- Lifetime = object lifetime

##### C++:
- Object may live on stack or heap

##### Java:
- Object always on heap
- Default values assigned

---

#### 3.3 Static / Class Variable
- Belongs to class, not object
- Single shared copy
- Shared across all instances

##### C++:
- Static storage duration
- Lifetime = entire program

##### Java:
- Initialized during class initialization
- Lifetime = until class unloading (usually program lifetime)

Static does NOT imply thread safety.

---

#### 3.4 Global Variable (C++)
- Declared outside functions/classes
- Static storage duration
- Lifetime = entire program
- Visibility depends on linkage

Excessive global state reduces modularity.

---

### 4. Declaration vs Initialization
#### Declaration
Defines type and introduces name.

#### Initialization
Assigns first value.

Declaration does not always imply initialization.
Behavior depends on storage duration and language rules.

---

### 5. Language Differences
---

#### C++
- True global variables supported
- Local variables not auto-initialized
- Global/static zero-initialized
- Stack and heap objects
- Supports references and pointers
- Multiple storage durations

---
#### Java
- No true global variables
- Local variables must be initialized
- Instance/static get default values
- Objects conceptually heap-allocated
- Always pass-by-value (reference copied)
- Class loading defines static lifetime

---

### 6. Value vs Reference
#### Value variable
Stores actual data.

#### Reference variable
Stores address/reference to object.

##### C++:
- Objects can be stored directly
- Pointers → objects storing addresses
- References → aliases to existing objects

##### Java:
- Primitives → value
- Objects → reference 
- Method calls copy the reference value, not the object

Java does not support pass-by-reference.

---

### 7. Parameter Passing
- Pass-by-value → copy is passed.
- Pass-by-reference → Original variable is accessed.

#### C++:
- Supports value, reference, and pointer semantics.

#### Java:
- Only pass-by-value.
- When passing objects, the reference is copied.

Reassigning parameter inside method does not change caller variable in Java.

---

### 8. Variable Shadowing
Occurs when inner scope redeclares a variable with same name.

- Inner variable hides outer variable.
- May cause subtle bugs.

> Avoid unnecessary shadowing.

---

### 9. Conceptual Memory View (High-Level)
This model is simplified.
- Local variables → stack frame
- Instance variables → inside object (heap)
- Static/global variables → static storage area

Actual layout depends on compiler or JVM implementation.
Detailed memory mechanics belong in 02_MemoryModel.md.

---

## Quick Recall 

Variable =
Name + Type + Memory Binding + Scope + Lifetime + Mutability

---

Scope → where accessible

Lifetime → how long alive

Type → memory + operations

Mutability → change allowed or not

---

#### C++:
- Locals uninitialized
- Globals/static zero-initialized
- Stack + heap objects
- Supports references

#### Java:
- No true globals
- Locals must initialize
- Objects always heap
- Pass-by-value only

---

Local → block lifetime

Instance → object lifetime

Static → class/program lifetime

---