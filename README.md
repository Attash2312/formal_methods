# formal_methods

# Z Notation & VDM-SL Cheatsheet (Pro Edition)

---

## Getting Started: Essential Concepts for Formal Methods

Before diving into Z Notation and VDM-SL, it's important to understand some basic mathematical and logical ideas that are used throughout formal methods. Here are the most important concepts, symbols, and their meanings:

### 1. Sets
- **Set:** A collection of distinct objects. Example: `{1, 2, 3}`. Think of a set as a basket holding unique items.
- **Subset (⊆):** A is a subset of B if every element of A is also in B. Example: `{1,2} ⊆ {1,2,3}` (True). If you have a basket of apples and oranges, a basket with just apples is a subset.
- **Proper Subset (⊂):** A is a proper subset of B if A ⊆ B and A ≠ B. Example: `{1,2} ⊂ {1,2,3}` (True).
- **Element of (∈):** Checks if an item is in a set. Example: `2 ∈ {1,2,3}` (True). Like checking if a book is in a library.
- **Not element of (∉):** Checks if an item is not in a set. Example: `4 ∉ {1,2,3}` (True).
- **Union (∪):** Combines all elements from two sets. Example: `{1,2} ∪ {2,3} = {1,2,3}`. Like merging two friend groups.
- **Intersection (∩):** Elements common to both sets. Example: `{1,2} ∩ {2,3} = {2}`. Like friends you have in common with someone else.
- **Difference (∖):** Elements in one set but not the other. Example: `{1,2,3} ∖ {2,3} = {1}`. Like removing borrowed books from your collection.

### 2. Relations and Functions
- **Relation (↔):** Links elements from one set to another. Example: `R = {(1, 'a'), (2, 'b')}`. Like a list of who is friends with whom.
- **Function (↦):** Assigns each element from one set to exactly one element in another. Example: `f = {1 ↦ 'a', 2 ↦ 'b'}`. Like assigning each student to a locker.
- **Map (⟶):** Every element in the first set has a value in the second set. Example: `f: ℕ ⟶ ℕ` means every natural number maps to a natural number.
- **Partial Map (⤔):** Some elements in the first set may not have a value. Example: `f: ℕ ⤔ ℕ`.
- **Domain (dom):** All keys in a map. Example: `dom {1 ↦ 'a', 2 ↦ 'b'} = {1,2}`.
- **Range (ran):** All values in a map. Example: `ran {1 ↦ 'a', 2 ↦ 'b'} = {'a','b'}`.

### 3. Logic
- **Predicate:** A statement that can be true or false. Example: `x > 0`. Like a rule: "Is the number positive?"
- **For all (∀):** The statement is true for every element. Example: `∀ x ∈ {1,2,3} • x > 0` (True). Like saying "All students passed."
- **There exists (∃):** The statement is true for at least one element. Example: `∃ x ∈ {1,2,3} • x = 2` (True). Like "At least one student got an A."
- **And (∧):** Both statements must be true. Example: `x > 0 ∧ y > 0`. Like "It is sunny AND warm."
- **Or (∨):** At least one statement is true. Example: `x = 0 ∨ y = 0`. Like "It is raining OR snowing."
- **Not (¬):** The opposite of a statement. Example: `¬(x > 0)`. Like "It is NOT raining."
- **Implies (⇒):** If the first is true, the second must be true. Example: `x > 0 ⇒ y > 0`. Like "If you study, you will pass."

### 4. Formal Specification
- **Formal methods** use math and logic to describe what a system should do, without ambiguity. Think of it as writing a contract for a system.
- **State:** The data or variables that describe the system at a point in time. Like the current contents of a shopping cart.
- **Operation:** How the state changes (e.g., deposit money, add item to cart).
- **Invariant:** A rule that must always be true (e.g., balance ≥ 0). Like "The cart can never have negative items."

---

## Table of Contents
1. [Getting Started: Essential Concepts for Formal Methods](#getting-started-essential-concepts-for-formal-methods)
2. [Z Notation: Concepts, Symbols & How to Write](#z-notation-concepts-symbols--how-to-write)
3. [Z Notation: Long Exam-Style Questions & Solutions](#z-notation-long-exam-style-questions--solutions)
4. [VDM-SL: Concepts, Symbols & How to Write](#vdm-sl-concepts-symbols--how-to-write)
5. [VDM-SL: Long Exam-Style Questions & Solutions](#vdm-sl-long-exam-style-questions--solutions)
6. [UML to VDM-SL Example (with Diagram)](#uml-to-vdm-sl-example-with-diagram)
7. [Exam Tips & Common Pitfalls](#exam-tips--common-pitfalls)
8. [Z vs VDM-SL: Comparison Table](#z-vs-vdm-sl-comparison-table)

---

## Z Notation: Concepts, Symbols & How to Write

**Z Notation** is a formal language for describing and reasoning about computer systems. It uses math and logic to make system requirements precise and unambiguous.

### Key Concepts
- **Schema:** A box that groups variables (state) and rules (predicates) about them.
- **State Schema:** Describes the current system state (what data is stored).
- **Operation Schema:** Describes how the state changes (with Δ) or stays the same (with Ξ).
- **Predicate:** A logical rule or condition (e.g., `x > 0`).
- **Inputs/Outputs:** Use `?` for input variables, `!` for output variables.
- **Prime (') Notation:** Shows the new value of a variable after an operation.

### How to Write a Z Schema
```
+-------------------------------+
|         SchemaName            |
|-------------------------------|
| variables: Type               |
| ...                           |
|-------------------------------|
| rules (predicates)            |
| ...                           |
+-------------------------------+
```
- **State schemas**: List all state variables and rules that must always be true.
- **Operation schemas**: Use ΔStateName for state change, ΞStateName for no change, and list all inputs/outputs and rules.

### Common Z Symbols & Operators (Beginner-Friendly)
| Symbol/Operator | Name/Meaning         | Example                | Explanation |
|-----------------|---------------------|------------------------|-------------|
| ℕ               | Natural numbers     | `x: ℕ`                 | Whole numbers starting from 0 (0, 1, 2, ...). Used for counts, IDs, etc. |
| ℤ               | Integers            | `y: ℤ`                 | All whole numbers, positive and negative (..., -2, -1, 0, 1, 2, ...). Useful for balances, temperatures, etc. |
| ℙ X             | Power set of X      | `A: ℙ ℕ`               | All possible subsets of X. If X = {1,2}, ℙ X = {∅, {1}, {2}, {1,2}}. Used for groups, collections. |
| ↦               | Map (function)      | `{a ↦ b}`              | Pairs a value from one set to a value in another (like a key-value pair in a dictionary). |
| ↔               | Relation            | `R: A ↔ B`             | Any set of pairs from A to B (not necessarily unique). Used for assignments, links. |
| ∈               | Element of          | `x ∈ A`                | Checks if x is in set A. Example: `2 ∈ {1,2,3}` is true. |
| ∉               | Not element of      | `x ∉ A`                | Checks if x is not in set A. Example: `4 ∉ {1,2,3}` is true. |
| ∪               | Union               | `A ∪ B`                | All elements from both sets. Example: `{1,2} ∪ {2,3} = {1,2,3}`. |
| ∩               | Intersection        | `A ∩ B`                | Only elements in both sets. Example: `{1,2} ∩ {2,3} = {2}`. |
| ∖               | Set difference      | `A ∖ B`                | Elements in A but not in B. Example: `{1,2,3} ∖ {2,3} = {1}`. |
| dom             | Domain              | `dom f`                | All keys in a map. Example: `dom {1 ↦ 'a', 2 ↦ 'b'} = {1,2}`. |
| ran             | Range               | `ran f`                | All values in a map. Example: `ran {1 ↦ 'a', 2 ↦ 'b'} = {'a','b'}`. |
| ∀               | For all             | `∀ x: ℕ • x > 0`       | Rule must be true for every x. Example: `∀ x ∈ {1,2,3} • x > 0` is true. |
| ∃               | There exists        | `∃ x: ℕ • x = 2`       | True for at least one x. Example: `∃ x ∈ {1,2,3} • x = 2` is true. |
| ¬               | Not                 | `¬(x > 0)`             | The opposite of a statement. Example: `¬(2 > 3)` is true. |
| ∧               | And                 | `x > 0 ∧ y > 0`        | Both must be true. Example: `2 > 0 ∧ 3 > 0` is true. |
| ∨               | Or                  | `x = 0 ∨ y = 0`        | At least one is true. Example: `2 = 0 ∨ 3 = 0` is false. |
| ⇒               | Implies             | `x > 0 ⇒ y > 0`        | If left is true, right must be true. |
| '               | Prime (next state)  | `balance' = ...`       | The value after an operation (e.g., new balance after deposit). |
| ?               | Input variable      | `amount?: ℕ`           | ? means input to an operation. Example: `amount?` is the input value. |
| !               | Output variable     | `result!: ℕ`           | ! means output/result from an operation. |
| Δ X             | State change        | `ΔBank`                | Indicates the state changes. |
| Ξ X             | No change           | `ΞBank`                | Indicates the state does not change. |
| bag X           | Multiset            | `stock: bag Item`      | Like a set, but allows repeated items (e.g., 3 apples). |
| λ               | Lambda (function)   | `λ x: ℕ • x+1`         | A way to write a function without naming it. |
| ⊎               | Bag union           | `b1 ⊎ b2`              | Combines two bags (adds up counts of items). |
| ⊆               | Subset              | `A ⊆ B`                | All elements of A are in B. Example: `{1,2} ⊆ {1,2,3}`. |
| ⊂               | Proper subset       | `A ⊂ B`                | A is a subset of B and A ≠ B. |
| ⟶               | Total function      | `A ⟶ B`                | Every A has a B. Example: `f: ℕ ⟶ ℕ` means every natural number maps to a natural number. |
| ⤔               | Partial function    | `A ⤔ B`                | Some A may not have a B. |

---

## Z Notation: Long Exam-Style Questions & Solutions

### 1. Bank Account System
**Description:**
A bank system has a balance. It supports deposit and withdrawal. The balance cannot go negative.

**State Schema:**
```
+-------------------+
|   Bank            |
|-------------------|
| balance: ℕ        |
|-------------------|
| balance ≥ 0       |
+-------------------+
```
**Initialization Schema:**
```
+-------------------+
|   InitBank        |
|-------------------|
| Bank              |
|-------------------|
| balance = 0       |
+-------------------+
```
**Operation Schemas:**
```
+-------------------+
|   Deposit         |
|-------------------|
| ΔBank             |
| amount?: ℕ        |
|-------------------|
| balance' = balance + amount? |
+-------------------+

+-------------------+
|   Withdraw        |
|-------------------|
| ΔBank             |
| amount?: ℕ        |
|-------------------|
| amount? ≤ balance |
| balance' = balance - amount? |
+-------------------+
```
**Explanation:**
- The state schema defines the variable and its invariant.
- The initialization sets the starting balance.
- Each operation is boxed, with clear preconditions and post-state.

---

### 2. Hospital Patient Management System
**Description:**
A hospital manages patients and their assigned rooms. Each patient can only be in one room at a time. Rooms are unique and can only be assigned to one patient. The hospital can admit, transfer, and discharge patients.

**State Schema:**
```
+--------------------------+
|   Hospital               |
|--------------------------|
| patients: ℙ PATIENT      |
| rooms: ℙ ROOM            |
| assigned: PATIENT ↦ ROOM |
|--------------------------|
| dom assigned ⊆ patients  |
| ran assigned ⊆ rooms     |
+--------------------------+
```
**Operation Schemas:**
```
+--------------------------+
|   Admit                  |
|--------------------------|
| ΔHospital                |
| p?: PATIENT              |
| r?: ROOM                 |
|--------------------------|
| p? ∉ patients ∧ r? ∈ rooms ∧ r? ∉ ran assigned |
| patients' = patients ∪ {p?} |
| assigned' = assigned ∪ {p? ↦ r?} |
+--------------------------+

+--------------------------+
|   Transfer               |
|--------------------------|
| ΔHospital                |
| p?: PATIENT              |
| r?: ROOM                 |
|--------------------------|
| p? ∈ dom assigned ∧ r? ∈ rooms ∧ r? ∉ ran assigned |
| assigned' = (assigned ∖ {p? ↦ assigned(p?)}) ∪ {p? ↦ r?} |
+--------------------------+

+--------------------------+
|   Discharge              |
|--------------------------|
| ΔHospital                |
| p?: PATIENT              |
|--------------------------|
| p? ∈ dom assigned        |
| assigned' = assigned ∖ {p? ↦ assigned(p?)} |
| patients' = patients ∖ {p?} |
+--------------------------+
```
**Explanation:**
- Admit adds a new patient and assigns a room.
- Transfer moves a patient to a new room.
- Discharge removes a patient and their room assignment.

---

### 3. Library Borrowing System
**Description:**
A library allows members to borrow books. Each book can be borrowed by only one member at a time. Members can borrow multiple books, but not the same book twice. Books must be available to be borrowed. The system supports borrowing and returning books.

**State Schema:**
```
+-------------------------------+
|   Library                     |
|-------------------------------|
| books: ℙ BOOK                 |
| members: ℙ MEMBER             |
| borrowed: BOOK ↦ MEMBER       |
|-------------------------------|
| dom borrowed ⊆ books          |
| ran borrowed ⊆ members        |
+-------------------------------+
```
**Operation Schemas:**
```
+-------------------------------+
|   BorrowBook                  |
|-------------------------------|
| ΔLibrary                      |
| b?: BOOK                      |
| m?: MEMBER                    |
|-------------------------------|
| b? ∈ books ∧ m? ∈ members ∧ b? ∉ dom borrowed |
| borrowed' = borrowed ∪ {b? ↦ m?} |
+-------------------------------+

+-------------------------------+
|   ReturnBook                  |
|-------------------------------|
| ΔLibrary                      |
| b?: BOOK                      |
|-------------------------------|
| b? ∈ dom borrowed             |
| borrowed' = borrowed ∖ {b? ↦ borrowed(b?)} |
+-------------------------------+
```
**Explanation:**
- BorrowBook allows a member to borrow an available book.
- ReturnBook makes a borrowed book available again.

---

### 4. University Exam Registration
**Description:**
A university allows students to register for exams. Each student can register for multiple exams, but only once per exam. Exams have a maximum capacity. The system supports registration and cancellation.

**State Schema:**
```
+--------------------------------------+
|   University                        |
|--------------------------------------|
| students: ℙ STUDENT                  |
| exams: ℙ EXAM                        |
| registered: STUDENT ↔ EXAM           |
| capacity: EXAM ↦ ℕ                   |
|--------------------------------------|
| dom registered ⊆ students            |
| ran registered ⊆ exams               |
| ∀ e: EXAM • #(registered∼[{e}]) ≤ capacity(e) |
+--------------------------------------+
```
**Operation Schemas:**
```
+--------------------------------------+
|   RegisterExam                       |
|--------------------------------------|
| ΔUniversity                          |
| s?: STUDENT                          |
| e?: EXAM                             |
|--------------------------------------|
| s? ∈ students ∧ e? ∈ exams ∧ (s?, e?) ∉ registered |
| #(registered∼[{e?}]) < capacity(e?)  |
| registered' = registered ∪ {(s?, e?)} |
+--------------------------------------+

+--------------------------------------+
|   CancelExam                         |
|--------------------------------------|
| ΔUniversity                          |
| s?: STUDENT                          |
| e?: EXAM                             |
|--------------------------------------|
| (s?, e?) ∈ registered                |
| registered' = registered ∖ {(s?, e?)} |
+--------------------------------------+
```
**Explanation:**
- RegisterExam checks capacity and prevents duplicate registration.
- CancelExam removes a student from an exam.

---

### 5. Airport Flight Management System
**Description:**
An airport manages flights and gates. Each flight can be assigned to one gate at a time, and each gate can only serve one flight at a time. The system supports assigning flights to gates, releasing gates, and transferring flights between gates.

**State Schema:**
```
+-------------------------------+
|   Airport                     |
|-------------------------------|
| flights: ℙ FLIGHT             |
| gates: ℙ GATE                 |
| assignment: FLIGHT ↦ GATE     |
|-------------------------------|
| dom assignment ⊆ flights      |
| ran assignment ⊆ gates        |
+-------------------------------+
```
**Operation Schemas:**
```
+-------------------------------+
|   AssignGate                  |
|-------------------------------|
| ΔAirport                      |
| f?: FLIGHT                    |
| g?: GATE                      |
|-------------------------------|
| f? ∈ flights ∧ g? ∈ gates ∧ f? ∉ dom assignment ∧ g? ∉ ran assignment |
| assignment' = assignment ∪ {f? ↦ g?} |
+-------------------------------+

+-------------------------------+
|   ReleaseGate                 |
|-------------------------------|
| ΔAirport                      |
| g?: GATE                      |
|-------------------------------|
| g? ∈ ran assignment           |
| assignment' = {f ↦ a | f ∈ dom assignment ∧ assignment(f) ≠ g? • f ↦ assignment(f)} |
+-------------------------------+

+-------------------------------+
|   TransferFlight              |
|-------------------------------|
| ΔAirport                      |
| f?: FLIGHT                    |
| g?: GATE                      |
|-------------------------------|
| f? ∈ dom assignment ∧ g? ∈ gates ∧ g? ∉ ran assignment |
| assignment' = (assignment ∖ {f? ↦ assignment(f?)}) ∪ {f? ↦ g?} |
+-------------------------------+
```
**Explanation:**
- AssignGate assigns a flight to an available gate.
- ReleaseGate frees a gate from its assigned flight.
- TransferFlight moves a flight to a new, unassigned gate.

---

### 9. Library Reservation System
**Description:**
A library allows members to reserve books. Each book can be reserved by only one member at a time. Members can reserve multiple books, but not the same book twice. Books must be available to be reserved. The system supports reserving and cancelling reservations.

**State Schema:**
```
+---------------------------------------+
|              Library                  |
|---------------------------------------|
| books: ℙ BOOK                         |
| members: ℙ MEMBER                     |
| reserved: BOOK ↦ MEMBER               |
|---------------------------------------|
| dom reserved ⊆ books                  |
| ran reserved ⊆ members                |
+---------------------------------------+
```
**Operation Schemas:**
```
+---------------------------------------+
|           ReserveBook                 |
|---------------------------------------|
| ΔLibrary                              |
| b?: BOOK                              |
| m?: MEMBER                            |
|---------------------------------------|
| b? ∈ books ∧ m? ∈ members ∧ b? ∉ dom reserved |
| reserved' = reserved ∪ {b? ↦ m?}      |
+---------------------------------------+

+---------------------------------------+
|           CancelReservation           |
|---------------------------------------|
| ΔLibrary                              |
| b?: BOOK                              |
|---------------------------------------|
| b? ∈ dom reserved                     |
| reserved' = reserved ∖ {b? ↦ reserved(b?)} |
+---------------------------------------+
```
**Explanation:**
- ReserveBook allows a member to reserve an available book.
- CancelReservation makes a reserved book available again.

---

### 10. Parking Lot Management
**Description:**
A parking lot manages cars and parking spots. Each spot can be occupied by only one car at a time. The system supports parking, moving, and removing cars.

**State Schema:**
```
+---------------------------------------+
|             ParkingLot                |
|---------------------------------------|
| spots: ℙ SPOT                         |
| cars: ℙ CAR                           |
| parked: SPOT ↦ CAR                    |
|---------------------------------------|
| dom parked ⊆ spots                    |
| ran parked ⊆ cars                     |
+---------------------------------------+
```
**Operation Schemas:**
```
+---------------------------------------+
|              ParkCar                  |
|---------------------------------------|
| ΔParkingLot                           |
| s?: SPOT                              |
| c?: CAR                               |
|---------------------------------------|
| s? ∈ spots ∧ c? ∈ cars ∧ s? ∉ dom parked ∧ c? ∉ ran parked |
| parked' = parked ∪ {s? ↦ c?}          |
+---------------------------------------+

+---------------------------------------+
|              MoveCar                  |
|---------------------------------------|
| ΔParkingLot                           |
| s1?: SPOT                             |
| s2?: SPOT                             |
|---------------------------------------|
| s1? ∈ dom parked ∧ s2? ∈ spots ∧ s2? ∉ dom parked |
| parked' = (parked ∖ {s1? ↦ parked(s1?)}) ∪ {s2? ↦ parked(s1?)} |
+---------------------------------------+

+---------------------------------------+
|             RemoveCar                 |
|---------------------------------------|
| ΔParkingLot                           |
| s?: SPOT                              |
|---------------------------------------|
| s? ∈ dom parked                       |
| parked' = parked ∖ {s? ↦ parked(s?)}  |
+---------------------------------------+
```
**Explanation:**
- ParkCar assigns a car to an available spot.
- MoveCar moves a car from one spot to another.
- RemoveCar frees a spot.

---

### 11. Employee Payroll System
**Description:**
A company manages employees and their salaries. Each employee has a unique ID and a salary. The system supports adding employees, updating salaries, and removing employees.

**State Schema:**
```
+---------------------------------------+
|             Payroll                   |
|---------------------------------------|
| employees: ℙ EMPLOYEE                 |
| salary: EMPLOYEE ↦ ℕ                  |
|---------------------------------------|
| dom salary ⊆ employees                |
| ∀ e: EMPLOYEE • e ∈ dom salary ⇒ salary(e) ≥ 0 |
+---------------------------------------+
```
**Operation Schemas:**
```
+---------------------------------------+
|           AddEmployee                 |
|---------------------------------------|
| ΔPayroll                              |
| e?: EMPLOYEE                          |
| s?: ℕ                                 |
|---------------------------------------|
| e? ∉ employees ∧ s? ≥ 0               |
| employees' = employees ∪ {e?}         |
| salary' = salary ∪ {e? ↦ s?}          |
+---------------------------------------+

+---------------------------------------+
|           UpdateSalary                |
|---------------------------------------|
| ΔPayroll                              |
| e?: EMPLOYEE                          |
| s?: ℕ                                 |
|---------------------------------------|
| e? ∈ employees ∧ s? ≥ 0               |
| salary' = salary ∪ {e? ↦ s?}          |
+---------------------------------------+

+---------------------------------------+
|           RemoveEmployee              |
|---------------------------------------|
| ΔPayroll                              |
| e?: EMPLOYEE                          |
|---------------------------------------|
| e? ∈ employees                        |
| employees' = employees ∖ {e?}         |
| salary' = salary ∖ {e? ↦ salary(e?)}  |
+---------------------------------------+
```
**Explanation:**
- AddEmployee adds a new employee with a salary.
- UpdateSalary changes an employee's salary.
- RemoveEmployee deletes an employee and their salary.

---

### 12. Student Grading System
**Description:**
A school manages students and their grades for courses. Each student can have a grade for each course. The system supports adding grades, updating grades, and removing grades.

**State Schema:**
```
+---------------------------------------+
|             Grading                   |
|---------------------------------------|
| students: ℙ STUDENT                   |
| courses: ℙ COURSE                     |
| grades: (STUDENT × COURSE) ↦ ℕ        |
|---------------------------------------|
| dom grades ⊆ students × courses       |
| ∀ (s, c): STUDENT × COURSE • (s, c) ∈ dom grades ⇒ grades((s, c)) ≥ 0 |
+---------------------------------------+
```
**Operation Schemas:**
```
+---------------------------------------+
|             AddGrade                  |
|---------------------------------------|
| ΔGrading                              |
| s?: STUDENT                           |
| c?: COURSE                            |
| g?: ℕ                                 |
|---------------------------------------|
| s? ∈ students ∧ c? ∈ courses ∧ g? ≥ 0 |
| grades' = grades ∪ {(s?, c?) ↦ g?}    |
+---------------------------------------+

+---------------------------------------+
|            UpdateGrade                |
|---------------------------------------|
| ΔGrading                              |
| s?: STUDENT                           |
| c?: COURSE                            |
| g?: ℕ                                 |
|---------------------------------------|
| (s?, c?) ∈ dom grades ∧ g? ≥ 0        |
| grades' = grades ∪ {(s?, c?) ↦ g?}    |
+---------------------------------------+

+---------------------------------------+
|            RemoveGrade                |
|---------------------------------------|
| ΔGrading                              |
| s?: STUDENT                           |
| c?: COURSE                            |
|---------------------------------------|
| (s?, c?) ∈ dom grades                 |
| grades' = grades ∖ {(s?, c?) ↦ grades((s?, c?))} |
+---------------------------------------+
```
**Explanation:**
- AddGrade assigns a grade to a student for a course.
- UpdateGrade changes a student's grade for a course.
- RemoveGrade deletes a grade entry.

---

## VDM-SL: Concepts, Symbols & How to Write

**VDM-SL** (Vienna Development Method - Specification Language) is a formal method for specifying and modeling systems using typed variables, invariants, and pre/post conditions.

### Key Concepts
- **State Block:** Defines system variables and invariants.
- **Operation:** Describes how the state changes, with pre/post conditions.
- **Function:** No side effects, just returns a value.
- **Invariant:** A condition that must always hold for the state.
- **Pre/Post:** Preconditions and postconditions for operations.
- **Old Value (~):** Refers to the value before the operation.

### How to Write a VDM-SL State & Operation
```
---------------------------------
state Name of
  var1: type1
  var2: type2
inv mk_Name(v1, v2) == ...;
---------------------------------

---------------------------------
operations
OpName(params)
pre ...
post ...;
---------------------------------
```
- **State block**: List all variables and invariants.
- **Operation**: List parameters, pre/post conditions, and use old value (~) as needed.

### Common VDM-SL Symbols & Operators
| Symbol/Operator | Name/Meaning         | Example                | Explanation |
|-----------------|---------------------|------------------------|-------------|
| nat             | Natural numbers     | `x: nat`               | Non-negative integers |
| int             | Integers            | `y: int`               | All integers |
| set of T        | Set                 | `A: set of nat`        | Unordered collection |
| seq of T        | Sequence            | `s: seq of int`        | Ordered collection |
| map T to U      | Map                 | `m: map nat to int`    | Key-value pairs |
| dom, rng        | Domain, Range       | `dom m`, `rng m`       | Keys/values of map |
| =, <>           | Equal, not equal    | `x = 5`, `x <> 0`      | Comparison |
| in set, not in set | Membership        | `x in set A`           | Set ops |
| union, inter, \ | Union, Intersect, Diff | `A union B`, ... | Set ops |
| card            | Cardinality         | `card s`               | Size of set/seq |
| ++              | Map override        | `m ++ {k |-> v}`       | Update/add entry |
| ~               | Old value           | `balance~`             | Value before op |
| forall, exists  | Quantifiers         | `forall x in set S & ...` | Logic |
| let ... in ...  | Local definition    | `let x = 2 in x+1`     | Temp var |
| if ... then ... else ... | Conditional | `if x > 0 then y else z` | Branching |
| mk_Type         | Constructor         | `mk_Bank(10)`          | Create record |
| inv mk_Type     | Invariant           | `inv mk_Bank(b) == b >= 0` | State constraint |
| pre/post        | Pre/Postcondition   | `pre x > 0 post y = x+1` | Op contract |
| RESULT          | Function result     | `post RESULT = x*x`    | Return value |

---

## VDM-SL: Long Exam-Style Questions & Solutions

### 1. Simple Bank Account
**Description:**
A bank account has a balance. Withdrawals cannot make the balance negative.

**State Block:**
```
---------------------------------
state Bank of
  balance: nat
inv mk_Bank(b) == b >= 0;
---------------------------------
```
**Operation:**
```
---------------------------------
operations
Withdraw(amount: nat)
pre amount <= balance
post balance = balance~ - amount;
---------------------------------
```
**Explanation:**
- The state block defines the variable and invariant.
- The operation block shows the precondition and postcondition.

---

### 2. Hospital Patient Management System
**Description:**
A hospital manages patients and their assigned rooms. Each patient can only be in one room at a time. Rooms are unique and can only be assigned to one patient. The hospital can admit, transfer, and discharge patients.

**State Block:**
```
---------------------------------
types
  Patient = token;
  Room = token;

state Hospital of
  patients: set of Patient
  rooms: set of Room
  assigned: map Patient to Room
inv mk_Hospital(p, r, a) == dom a subset p and rng a subset r;
---------------------------------
```
**Operations:**
```
---------------------------------
operations
Admit(p: Patient, r: Room)
pre p not in set patients and r in set rooms and r not in set rng assigned
post patients = patients~ union {p} and assigned = assigned~ ++ {p |-> r};

Transfer(p: Patient, r: Room)
pre p in set dom assigned and r in set rooms and r not in set rng assigned
post assigned' = (assigned ∖ {p ↦ assigned(p)}) ∪ {p ↦ r};

Discharge(p: Patient)
pre p in set dom assigned
post assigned' = assigned ∖ {p? ↦ assigned(p?)} |
patients' = patients ∖ {p?} |
---------------------------------
```
**Explanation:**
- Admit adds a new patient and assigns a room.
- Transfer moves a patient to a new room.
- Discharge removes a patient and their room assignment.

---

### 3. Library Borrowing System
**Description:**
A library allows members to borrow books. Each book can be borrowed by only one member at a time. Members can borrow multiple books, but not the same book twice. Books must be available to be borrowed. The system supports borrowing and returning books.

**State Block:**
```
---------------------------------
types
  Book = token;
  Member = token;

state Library of
  books: set of Book
  members: set of Member
  borrowed: map Book to Member
inv mk_Library(b, m, br) == dom br subset b and rng br subset m;
---------------------------------
```
**Operations:**
```
---------------------------------
operations
BorrowBook(b: Book, m: Member)
pre b in set books and m in set members and b not in set dom borrowed
post borrowed = borrowed~ ++ {b |-> m};

ReturnBook(b: Book)
pre b in set dom borrowed
post borrowed = {k |-> v | k in set dom borrowed~ and k <> b and v = borrowed~(k)};
---------------------------------
```
**Explanation:**
- BorrowBook allows a member to borrow an available book.
- ReturnBook makes a borrowed book available again.

---

### 4. University Exam Registration
**Description:**
A university allows students to register for exams. Each student can register for multiple exams, but only once per exam. Exams have a maximum capacity. The system supports registration and cancellation.

**State Block:**
```
---------------------------------
types
  Student = token;
  Exam = token;

state University of
  students: set of Student
  exams: set of Exam
  registered: map Student to set of Exam
  capacity: map Exam to nat
inv mk_University(s, e, r, c) == dom r subset s and rng c subset e;
---------------------------------
```
**Operations:**
```
---------------------------------
operations
RegisterExam(stu: Student, ex: Exam)
pre stu in set students and ex in set exams and (stu not in set dom registered or ex not in set registered~(stu)) and card {s | s in set dom registered~ and ex in set registered~(s)} < capacity(ex)
post registered = if stu in set dom registered~
  then registered~ ++ {stu |-> registered~(stu) union {ex}}
  else registered~ ++ {stu |-> {ex}};

CancelExam(stu: Student, ex: Exam)
pre stu in set dom registered and ex in set registered(stu)
post registered = registered~ ++ {stu |-> registered~(stu) \ {ex}};
---------------------------------
```
**Explanation:**
- RegisterExam checks capacity and prevents duplicate registration.
- CancelExam removes a student from an exam.

---

### 5. Airport Flight Management System
**Description:**
An airport manages flights and gates. Each flight can be assigned to one gate at a time, and each gate can only serve one flight at a time. The system supports assigning flights to gates, releasing gates, and transferring flights between gates.

**State Block:**
```
---------------------------------
types
  Flight = token;
  Gate = token;

state Airport of
  flights: set of Flight
  gates: set of Gate
  assignment: map Flight to Gate
inv mk_Airport(f, g, a) == dom a subset f and rng a subset g;
---------------------------------
```
**Operations:**
```
---------------------------------
operations
AssignGate(f: Flight, g: Gate)
pre f in set flights and g in set gates and f not in set dom assignment and g not in set rng assignment
post assignment = assignment~ ++ {f |-> g};

ReleaseGate(g: Gate)
pre g in set rng assignment
post assignment = {k |-> v | k in set dom assignment~ and assignment~(k) <> g and v = assignment~(k)};

TransferFlight(f: Flight, g: Gate)
pre f in set dom assignment and g in set gates and g not in set rng assignment
post assignment = (assignment~ \ {f |-> assignment~(f)}) ++ {f |-> g};
---------------------------------
```
**Explanation:**
- AssignGate assigns a flight to an available gate.
- ReleaseGate frees a gate from its assigned flight.
- TransferFlight moves a flight to a new, unassigned gate.

---

### 6. Online Shopping Cart System
**Description:**
An online store allows customers to add products to their cart. Each cart keeps track of the quantity of each product. Customers can add, remove, and clear products from their cart. The cart cannot have negative quantities.

**State Schema:**
```
+-------------------------------+
|   Cart                        |
|-------------------------------|
| products: ℙ PRODUCT           |
| cart: PRODUCT ↦ ℕ             |
|-------------------------------|
| dom cart ⊆ products           |
| ∀ p: PRODUCT • p ∈ dom cart ⇒ cart(p) > 0 |
+-------------------------------+
```
**Operation Schemas:**
```
+-------------------------------+
|   AddProduct                  |
|-------------------------------|
| ΔCart                         |
| p?: PRODUCT                   |
| qty?: ℕ                       |
|-------------------------------|
| p? ∈ products ∧ qty? > 0      |
| cart' = if p? ∈ dom cart then cart ⊎ {p? ↦ qty?} else cart ∪ {p? ↦ qty?} |
+-------------------------------+

+-------------------------------+
|   RemoveProduct               |
|-------------------------------|
| ΔCart                         |
| p?: PRODUCT                   |
| qty?: ℕ                       |
|-------------------------------|
| p? ∈ dom cart ∧ qty? > 0 ∧ cart(p?) ≥ qty? |
| cart' = if cart(p?) = qty? then cart ∖ {p? ↦ cart(p?)} else cart ⊎ {p? ↦ -qty?} |
+-------------------------------+

+-------------------------------+
|   ClearCart                   |
|-------------------------------|
| ΔCart                         |
|-------------------------------|
| cart ≠ ∅                      |
| cart' = ∅                     |
+-------------------------------+
```
**Explanation:**
- AddProduct increases the quantity or adds a new product.
- RemoveProduct decreases the quantity or removes the product if quantity is zero.
- ClearCart empties the cart.

---

### 7. Restaurant Order Management
**Description:**
A restaurant takes orders from customers. Each order is a bag (multiset) of dishes. Customers can place, update, and cancel orders. The menu lists all available dishes.

**State Block:**
```
---------------------------------
types
  Dish = token;
  Customer = token;

state Restaurant of
  menu: set of Dish
  orders: map Customer to map Dish to nat
inv mk_Restaurant(m, o) == forall c in set dom o & dom o(c) subset m and forall d in set dom o(c) & o(c)(d) > 0;
---------------------------------
```
**Operations:**
```
---------------------------------
operations
PlaceOrder(c: Customer, o: map Dish to nat)
pre dom o subset menu and card o > 0
post orders = orders~ ++ {c |-> o};

UpdateOrder(c: Customer, o: map Dish to nat)
pre c in set dom orders~ and dom o subset menu
post orders = orders~ ++ {c |-> o};

CancelOrder(c: Customer)
pre c in set dom orders~
post orders = {k |-> v | k in set dom orders~ and k <> c and v = orders~(k)};
---------------------------------
```
**Explanation:**
- PlaceOrder creates a new order for a customer.
- UpdateOrder changes an existing order.
- CancelOrder removes a customer's order.

---

### 8. Hotel Room Booking
**Description:**
A hotel manages rooms and guests. Each room can be booked by one guest at a time. Guests can book, check in, and check out. Only available rooms can be booked.

**State Block:**
```
---------------------------------
types
  Room = token;
  Guest = token;

state Hotel of
  rooms: set of Room
  guests: set of Guest
  booked: map Room to Guest
inv mk_Hotel(r, g, b) == dom b subset r and rng b subset g;
---------------------------------
```
**Operations:**
```
---------------------------------
operations
BookRoom(r: Room, g: Guest)
pre r in set rooms and g in set guests and r not in set dom booked and g not in set rng booked
post booked = booked~ ++ {r |-> g};

CheckIn(r: Room, g: Guest)
pre r in set dom booked and booked(r) = g
post booked = booked~;

CheckOut(r: Room)
pre r in set dom booked
post booked = {k |-> v | k in set dom booked~ and k <> r and v = booked~(k)};
---------------------------------
```
**Explanation:**
- BookRoom assigns a guest to an available room.
- CheckIn confirms the guest is in the correct room (no state change).
- CheckOut frees the room.

---

## UML to VDM-SL Example (with Diagram)

**UML Scenario:**
A UML class diagram shows a `Car` class with attributes `regNo: String`, `owner: String`, and a `Garage` class with a set of `Car` objects. The garage can add and remove cars. Each car's registration number must be unique in the garage.

**UML Class Diagram (ASCII):**
```
+-----------+           +-----------+
|   Car     |           |  Garage   |
|-----------|           |-----------|
| regNo     |<>---------| cars:     |
| owner     |           | set of Car|
+-----------+           +-----------+
```
- `Garage` has a set of `Car` objects (composition, shown by <>).
- Each `Car` has `regNo` and `owner` attributes.

**Step-by-Step VDM-SL Model:**
```
---------------------------------
types
  Car :: regNo: String
          owner: String;

state Garage of
  cars: set of Car
inv mk_Garage(cs) == forall c1, c2 in set cs & c1 <> c2 => c1.regNo <> c2.regNo;
---------------------------------

---------------------------------
operations
AddCar(c: Car)
pre forall car in set cars~ & car.regNo <> c.regNo
post cars = cars~ union {c};

RemoveCar(reg: String)
pre exists car in set cars~ & car.regNo = reg
post cars = {car | car in set cars~ & car.regNo <> reg};
---------------------------------
```
**Explanation:**
- The state invariant ensures all registration numbers are unique.
- Operations add and remove cars by registration number.

---

## Exam Tips & Common Pitfalls
- Always define types and invariants clearly.
- Use schemas/states with invariants for safety.
- Add inputs/outputs to all operations.
- Check pre/post conditions for every operation.
- For Z:
  - Use schema inclusion for modularity.
  - Bags for counting, sets for uniqueness.
  - Chaining schemas for complex operations.
- For VDM-SL:
  - Always keep domain/range valid in maps.
  - Use map override (`++`) for updates.
  - Write invariants for all states.
- For UML to VDM:
  - Map classes to types/records.
  - Map associations to sets/maps.
  - Enforce uniqueness with invariants.

---

## Z vs VDM-SL: Comparison Table

| Feature         | Z Notation         | VDM-SL                |
|-----------------|--------------------|-----------------------|
| Foundation      | Set theory, logic  | Typed algebraic specs |
| State           | Schemas            | State blocks          |
| Operations      | Operation schemas  | Operations/functions  |
| Invariants      | Predicates         | inv mk_Type           |
| Bags/Multisets  | `bag X`            | `map X to nat`        |
| Pre/Post        | Predicates         | pre/post clauses      |
| Refinement      | Supported          | Supported             |
| Tooling         | Z/Eves, CZT        | VDMTools, Overture    |

---

**Good luck on your Formal Methods exam!**

---

*Let me know if you want more practice problems, MCQs, or a mock test version!*

--- 
