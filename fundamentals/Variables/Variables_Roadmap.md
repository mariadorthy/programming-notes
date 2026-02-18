## Phase 1 — Foundations (This is syntax + behavioral understanding level.)

### Core Definition
    - Variable = Name + Type + Memory + Lifetime + Scope
    - Declaration vs Initialization
    - Mutability (const / final)

### Core Properties
    - Type
    - Scope
    - Lifetime
    - Mutability
    - Linkage (C++ focus)

### Categories of Variables
#### C++
    - Local
    - Global
    - Instance (class member)
    - Static (class-level)
    - Static vs Instance difference
    - Local vs Instance shadowing

#### Java
    - Local
    - Instance
    - Static (class variable)
    - No true global
    - Local vs Instance shadowing

### Initialization Behavior
    - C++: local uninitialized, global/static zero-initialized
    - Java: local must initialize, instance/static get defaults

### Memory Hint (High Level)
    - Stack → local
    - Heap → object
    - Static storage → static/global

### Value vs Reference
    - Primitive vs reference (Java)
    - Object direct vs pointer/reference (C++)

### Parameter Passing Basics
    - C++: value / reference
    - Java: pass-by-value (reference copied)

### Shadowing
    - This is strong foundational coverage.

## Phase 2 — Deep System Understanding (this is Memory, runtime, and system-level mechanics)
### Memory Model Deep Dive
#### C++
    - Stack vs Heap vs Static storage
    - Storage duration types:
        - automatic
        - static
        - dynamic
        - thread_local
    - Memory layout of program

#### Java
    - Stack frames
    - Heap
    - Method Area / Metaspace
    - String constant pool
    - Where static fields actually live

### Initialization Order
#### C++
    - Zero initialization
    - Constant initialization
    - Dynamic initialization
    - Static initialization order fiasco

#### Java
    - Class loading
    - Static fields
    - Static blocks
    - Instance fields
    - Instance initializer blocks
    - Constructor order

### Const vs Final vs constexpr
    - C++ const
    - constexpr
    - Compile-time constant vs runtime constant
    - Java final
    - static final compile-time constants

### Static Nuances
    - Static inside function (C++)
    - Static inside class (C++)
    - Static member functions
    - Static nested classes (Java)
    - Static blocks (Java)

### Thread Safety
    - Static variable shared across threads
    - Race conditions
    - Why static != safe
    - Synchronization basics

### Object Lifetime & Destruction
#### C++
    - Deterministic destruction
    - RAII
    - Destructor timing

#### Java
    - Garbage collection
    - Reachability
    - Finalize (historical)
    - Why destruction timing is unpredictable

### Compile-Time vs Runtime Behavior
    - Constant folding
    - Inlining
    - Class initialization triggers
    - Optimization differences
