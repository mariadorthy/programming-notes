# Variables — System-Level Understanding Roadmap
This roadmap is divided into two layers:

- **Phase 1 — Foundations** → Syntax + observable behavior
- **Phase 2 — Deep System Understanding** → Memory model, runtime mechanics, and compiler/JVM behavior

---

## Phase 1 — Foundations
**Focus:** What variables are, how they behave, and how languages expose them.

---

### 1. Core Definition
- Variable model
    - Name
    - Type
    - Memory binding
    - Scope
    - Lifetime
    - Mutability
- Declaration vs Initialization
- Mutability (`const` , `final`)

---

### 2. Core Properties
- Type
- Scope
- Lifetime
- Mutability
- Linkage (C++)

*Key separation to understand:*
- Scope ≠ Lifetime
- Lifetime ≠ Storage location
- Mutability ≠ Lifetime
- Linkage ≠ Scope

---

### 3. Categories of Variables

#### C++
- Local (automatic storage duration)
- Global
- Instance (class member)
- Static (class-level or function-level)
- Static vs Instance
- Variable Shadowing

---

#### Java
- Local
- Instance
- Static (class variable)
- No true global
- Variable Shadowing

---

### 4. Initialization Behavior
#### C++
- Local variables → uninitialized (indeterminate)
- Global/static → zero-initialized before dynamic initialization
- Static initialization order (high-level awareness)

#### Java
- Local variables must be explicitly initialized
- Instance/static fields receive default values
- Class loading triggers static initialization

### 5. Memory Model (High-Level Conceptual View)
- Stack (call frames)
- Heap (dynamic objects)
- Static storage area

        This is conceptual.
        Actual memory layout depends on compiler or JVM implementation.

---

### 6. Value vs Reference
#### Java
- Primitives → value
- Objects → reference 
- Passing an object copies the reference value, not the object

#### C++
- Objects can be stored directly (value semantics)
- Pointers → objects that store addresses
- References → aliases to existing objects (not reseatable)

---

### 7. Parameter Passing
#### C++
- Pass-by-value
- Pass-by-reference
- Pass-by-pointer

#### Java
- Always pass-by-value
- Object references are copied

---

### 8. Variable Shadowing
- Inner scope hides outer declaration
- `this` used to access instance member
- Can introduce subtle logic errors

---
---

## Phase 2 — Deep System Understanding
Focus: Runtime behavior, memory layout, compiler/JIT behavior, and edge cases.

### 1. Storage Duration & Allocation Model
#### C++ Storage Durations
- Automatic
- Static
- Dynamic
- Thread-local

---

#### Java Allocation Model
- Objects conceptually allocated on heap
- Local variables stored in stack frames
- Static fields associated with class metadata
*Advanced:*
- Escape analysis
- Stack allocation via JIT
- Scalar replacement

*Key insight:*
Even though Java specifies heap allocation conceptually, the JIT may optimize allocation away if the object does not escape.

---

### 2. Memory Layout Deep Dive
#### C++
- Program layout: text, data, bss, heap, stack
- Object memory layout basics
- Alignment and padding

#### Java
- Stack frames (per method call)
- Heap
- Metaspace (class metadata)
- String constant pool
- Static field storage

---

### 3. Initialization Order
#### C++
- Zero initialization
- Constant initialization
- Dynamic initialization
- Static initialization order problem

#### Java
- Class loading process
- Static field initialization
- Static blocks
- Instance field initialization
- Constructor execution order

---

### 4. Const / Final / Compile-Time Constants
#### C++
- `const`
- `constexpr`
- Compile-time vs runtime constant
- Internal linkage via `const`

#### Java
- `final` 
- `static final`
- Compile-time constant inlining

---

### 5. Static Semantics
#### C++
- Static inside function
- Static class members
- Static member functions
- Translation unit scope

#### Java
- Static fields
- Static methods
- Static nested classes
- Static blocks
- Class initialization triggers

---

### 6. Object Lifetime & Destruction
#### C++
- Deterministic destruction
- RAII
- Destructor timing
- Temporary object lifetime
- Move semantics impact 

#### Java
- Garbage collection
- Reachability graph
- GC eligibility
- Non-deterministic destruction
- Stop-the-world pauses (high level)

---

### 7. Concurrency & Shared State
- Static variables shared across threads
- Race conditions
- `static` ≠ thread-safe
- Synchronization fundamentals
- Memory visibility basics 

---

### 8. Compile-Time vs Runtime Behavior
- Constant folding
- Inlining
- Class initialization triggers
- Optimization differences (C++ vs JVM)
- JIT optimizations affecting variable allocation

---

## 9. Conceptual Separation (Critical Distinctions)
You must clearly separate the following concepts:
- **Scope** → Where a variable is accessible (compile-time visibility)
- **Lifetime** → How long a variable exists (runtime existence)
- **Storage Duration (C++)** → The rule that defines lifetime
- **Allocation Location** → Where memory physically resides (implementation detail)
- **Mutability** → Whether value changes are allowed (design constraint)
- **Linkage (C++)** → Cross-translation-unit visibility (link-time behavior)

    > Mixing these concepts indicates shallow understanding.