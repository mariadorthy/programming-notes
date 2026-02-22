# Variables — Complete System-Level Roadmap (C++)
This roadmap is divided into two phases:
- **Phase 1 — Language Foundations** 
- **Phase 2 — System & Runtime Mechanics** 

---

## Phase 1 — Foundations (Language-Level Behavior)
**Focus:** What the C++ language specifies and guarantees.

---

### 1. Variable Model 
A variable in C++ is defined by:
- Name binding
- Type
- Storage duration
- Scope
- Lifetime
- Mutability (`const`)
- Linkage
#### Conceptual Distinctions
- Scope ≠ Lifetime
- Lifetime ≠ Storage location
- Storage duration defines lifetime rule
- `const` ≠ compile-time constant
- Linkage ≠ Scope

---

### 2. Storage Duration (Language Rule)
C++ defines four storage durations:
- Automatic
- Static
- Dynamic
- Thread-local
Storage duration:
- Is defined by the language
- Determines when lifetime begins and ends
- Does not mandate physical memory layout.

---

### 3. Categories of Variables (C++)
- Local (automatic storage duration)
- Global
- Static local
- Static class member
- Non-static data member (instance variable)
- Thread-local (`thread_local`)
- Dynamic objects (`new`)
Each category influences:
- Storage duration
- Initialization behavior
- Linkage (where applicable)
- Lifetime characteristics

---

### 4. Initialization Rules (Precise Understanding Required)
- Default initialization
- Value initialization
- Zero initialization
- Direct initialization
- Copy initialization
- List initialization
#### Static initialization phases:
- Zero initialization
- Constant initialization
- Dynamic initialization

---

### 5. Name Lookup & Shadowing
- Block scope shadowing
- Class member shadowing
- `this` pointer 
- `::` scope resolution operator
- Name hiding vs overriding

---

### 6. Parameter Passing & Value Semantics
- Pass-by-value
- Pass-by-reference
- Pass-by-pointer
- Temporary lifetime extension via `const` reference
- Reference collapsing (overview)

---

### 7. Temporary Objects & Lifetime
- Prvalues and temporary objects
- Lifetime until end of full-expression
- Lifetime extension via `const` reference
- Common dangling scenarios

---
## Phase 2 — System & Runtime Mechanics
**Focus:** How implementations typically realize language rules.

---

### 8. Typical Implementation Memory Model (Non-Normative)
Common program layout in typical systems:
- Text segment
- Data segment
- BSS
- Heap
- Stack
This structure is common in real-world implementations but is not required by the C++ standard.

---

### 9. Object Lifetime Rules
- When lifetime begins (construction rules)
- When lifetime ends (destruction rules)
- Destructor timing
- Order of destruction
- Temporary destruction
- Dangling pointers
- Use-after-lifetime errors

---

### 10. Static Initialization Order 
- Cross-translation unit initialization
- Unspecified order across translation units
- Construct-on-first-use idiom

---

### 11. Const & Compile-Time Behavior
- `const`
- `constexpr`
- Constant expressions
- Internal linkage via `const`
- Compile-time vs runtime evaluation
- Constant folding (optimization awareness)

---

### 12. Linkage & Translation Units
- Internal linkage
- External linkage
- `extern`
- One Definition Rule (ODR)
- Multiple definition errors
- Inline variables (C++17)

---

### 13. Concurrency Awareness
- Static variables across threads
- Data races
- Memory visibility basics
- Thread-local storage 
- Initialization of function-local statics (since C++11 thread-safe)

---

### Mastery Check (Interview Level)
You should be able to answer clearly:
- Is storage duration a language rule or runtime behavior?
- Can lifetime exist without scope?
- Is storage duration equal to stack allocation?
- When exactly does object lifetime begin?
- What is the difference between zero initialization and value initialization?
- Why can static initialization order cause issues?
- Does const imply compile-time constant?
- Can an object exist without any named variable referring to it?
- Is stack guaranteed by the C++ standard?

---