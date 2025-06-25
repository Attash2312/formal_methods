# Formal Methods Past Papers & Quizzes

## Table of Contents
1. [Quiz Questions](#quiz-questions)
2. [2022 Spring Exam](#2022-spring-exam)
3. [2022 Exam](#2022-exam)
4. [2023 Exam](#2023-exam)

---

## Quiz Questions

### Quiz #1: Car Park System (Z Notation)
**CLO:** 2 - Apply the techniques used to formally specify software  
**Bloom Taxonomy Level:** Applying  
**Marks:** 5 + 5 = 10

**Problem:** A car park has a limited capacity. The number of cars currently occupying spaces is counted. When a car enters the park, the count increases, and when a car leaves, the count decreases. The system outputs the number of spaces left in the park.

**Type Declarations:**
- `capacity : ℤ`
- `capacity ≥ 0`
- `cars : ℤ`
- `cars ≥ 0`
- `cars ≤ capacity`

#### Solution:

**Schema Enter:**
```
Enter
  Δ(cars)
  cars' = cars + 1
  cars' ≤ capacity
```

**Schema Depart:**
```
Depart
  Δ(cars)
  cars' = cars - 1
  cars' ≥ 0
  spaces_left! = capacity - cars'
```

---

### Quiz #2: Class Manager Assistant (VDM Notation)
**CLO:** 3 - Apply the techniques used to formally design and verify whether a software product satisfies its specifications  
**Bloom Taxonomy Level:** Applying  
**Marks:** 10

**Problem:** Class Manager Assistant provides support for a class manager to admit students to a class and to record which of them have done the midterm exercises. The number of students can't exceed the LIMIT.

**UML Class Diagram:**
- **ClassManagerAssistant**
  - `reg: Student[*]`
  - `passed: Student[*]`
  - `Enroll()`
  - `Test()`

#### Solution:

**Type Declarations:**
```
types Student = <Student>
reg: set of Student
passed: set of Student
LIMIT: ℕ
```

**State Specification:**
```
State ClassManagerAssistant
  reg: set of Student
  passed: set of Student
  inv mk-ClassManagerAssistant(reg, passed) ==
    card reg ≤ LIMIT
```

**Operation Specifications:**
```
Operation Enroll(s: Student)
  ext wr reg: set of Student
  pre s ∉ reg
  post reg' = reg ∪ {s}

Operation Test()
  ext wr passed: set of Student
  pre true
  post passed' = passed ∪ {s | s ∈ reg}
```

---

### Quiz #3: Library Manager Assistant (VDM Notation)
**CLO:** 3  
**Bloom Taxonomy Level:** Applying  
**Total Marks:** 10

**Problem:** A Library manager's assistant provides support to a manager. The system provides the count of books on shelves and the count of books that are borrowed. The number of books on the shelves can't exceed the LIMIT.

**UML Class Diagram:**
- **LibraryManagerAssistant**
  - `bookCount: integer`
  - `borrowCount: integer`
  - `AddBook()`
  - `GetBorrowCount(): integer`

#### Solution:

**Type Declarations:**
```
types integer = ℤ
LIMIT: ℕ
```

**State Specification:**
```
State LibraryManagerAssistant
  bookCount: ℤ
  borrowCount: ℤ
  inv mk-LibraryManagerAssistant(bookCount, borrowCount) ==
    bookCount ≥ 0 ∧ borrowCount ≥ 0 ∧ bookCount ≤ LIMIT
```

**Operation Specifications:**
```
Operation AddBook()
  ext wr bookCount: ℤ
  pre bookCount < LIMIT
  post bookCount' = bookCount + 1

Operation GetBorrowCount(): integer
  ext rd borrowCount: ℤ
  pre true
  post RESULT = borrowCount
```

---

### Quiz #4: Class Manager Assistant (Duplicate)
**CLO:** 3  
**Bloom Taxonomy Level:** Applying  
**Total Marks:** 10

*Same as Quiz #2 - Class Manager Assistant*

---

## 2022 Spring Exam

### Question 1: University System (Z Notation)
**CLO:** 2  
**Marks:** 3+3+4=10

#### State Schema:
```
University
  students: ℙ PEOPLE
  subjects: ℙ SUBJECT
  enrolments: PEOPLE ↦ SUBJECT
  dom enrolments ⊆ students
  ran enrolments ⊆ subjects
```

#### Operation Schemas:

**newStudent:**
```
newStudent
  ΔUniversity
  pers?: PEOPLE
  students' = students ∪ {pers?}
  enrolments' = enrolments
  subjects' = subjects
```

**studentLeaves:**
```
studentLeaves
  ΔUniversity
  pers?: PEOPLE
  pers? ∈ students
  pers? ∉ dom enrolments
  students' = students \ {pers?}
  enrolments' = { p |-> s | p |-> s ∈ enrolments ∧ p ≠ pers? }
  subjects' = subjects
```

**personSubjects:**
```
personSubjects
  ΞUniversity
  pers?: PEOPLE
  subj!: ℙ SUBJECT
  pers? ∈ dom enrolments
  subj! = { s | pers? |-> s ∈ enrolments }
```

### Question 2: Seat Booking System (Z Notation)
**CLO:** 2  
**Marks:** 3+3+4=10

#### State Schema:
```
SeatBooking
  bookedTo: SEAT ↣ PERSON
  rdom bookedTo ≤ Limit
```

---

## 2022 Exam

### Question 01: Birthday Book (Z Notation)
**Marks:** 6+4=10  
**CLO:** 2

#### State Schema:
```
BirthdayBook
  known: ℙ NAME
  birthday: NAME ↣ DATE
  known = dom birthday
```

#### Operation Schemas:

**Add a Birthday:**
```
AddBirthday
  ΔBirthdayBook
  name?: NAME
  date?: DATE
  already_known!: BOOL
  name? ∈ known ⇒ (already_known! = TRUE ∧ known' = known ∧ birthday' = birthday)
  name? ∉ known ⇒ (already_known! = FALSE ∧ known' = known ∪ {name?} ∧ birthday' = birthday ⊕ {name? |-> date?})
```

**Find Birthday:**
```
FindBirthday
  ΞBirthdayBook
  name?: NAME
  date!: DATE
  name? ∈ known
  date! = birthday(name?)
```

### Question 2: Airport System (Z Notation)
**Marks:** 10  
**CLO:** 3

#### State Schema:
```
Airport
  permission: ℙ Aircraft
  landed: ℙ Aircraft
  #permission ≤ 20
  landed ⊆ permission
```

#### Operation Schemas:

**givePermission:**
```
givePermission
  ΔAirport
  aircraft?: Aircraft
  aircraft? ∉ permission
  permission' = permission ∪ {aircraft?}
  landed' = landed
```

**recordLanding:**
```
recordLanding
  ΔAirport
  aircraft?: Aircraft
  aircraft? ∈ permission
  landed' = landed ∪ {aircraft?}
  permission' = permission
```

**getPermission:**
```
getPermission
  ΞAirport
  aircrafts!: ℙ Aircraft
  aircrafts! = permission
```

**numberWaiting:**
```
numberWaiting
  ΞAirport
  count!: ℤ
  count! = #permission - #landed
```

### Question 03: Robot System (VDM Notation)
**Marks:** 1+1+2*4=10  
**CLO:** 4

#### (a) Type Declaration:
```
types Mode = <working> | <idle> | <broken>
```

#### (b) State Specification with Initialization:
```
State Robot
  mode: Mode
  init mk-Robot(m) == m = <idle>
```

#### (c) Operation Specifications:

**setMode:**
```
setMode(m?: Mode)
  ext wr mode: Mode
  pre true
  post mode' = m?
```

**getMode:**
```
getMode() m!: Mode
  ext rd mode: Mode
  pre true
  post m! = mode
```

**isIdle:**
```
isIdle() b!: Boolean
  ext rd mode: Mode
  pre true
  post b! = (mode = <idle>)
```

**Modified setMode:**
```
setMode(m?: Mode)
  ext wr mode: Mode
  pre (mode ≠ <broken> ∨ m? ≠ <working>) ∧ (mode ≠ <working> ∨ m? ≠ <broken>)
  post mode' = m?
```

### Question 04: Disk Scanner (VDM Notation)
**Marks:** 1+1+2*4=10  
**CLO:** 4

#### (a) Type Declaration:
```
types Block = TrackSector
  TrackSector :: track: ℤ
              sector: ℤ
```

#### (b) State Specification with Initialization:
```
State DiskScanner
  damagedBlocks: set of Block
  init mk-DiskScanner(db) == db = {}
```

#### (c) Operation Specifications:

**addBlock:**
```
addBlock(t?: ℤ, s?: ℤ)
  ext wr damagedBlocks: set of Block
  pre mk-TrackSector(t?, s?) ∉ damagedBlocks
  post damagedBlocks' = damagedBlocks ∪ {mk-TrackSector(t?, s?)}
```

**removeBlock:**
```
removeBlock(t?: ℤ, s?: ℤ)
  ext wr damagedBlocks: set of Block
  pre mk-TrackSector(t?, s?) ∈ damagedBlocks
  post damagedBlocks' = damagedBlocks \ {mk-TrackSector(t?, s?)}
```

**isDamaged:**
```
isDamaged(t?: ℤ, s?: ℤ) b!: Boolean
  ext rd damagedBlocks: set of Block
  pre true
  post b! = (mk-TrackSector(t?, s?) ∈ damagedBlocks)
```

**getBadSectors:**
```
getBadSectors(t?: ℤ) secs!: set of ℤ
  ext rd damagedBlocks: set of Block
  pre true
  post secs! = { s | mk-TrackSector(t?, s) ∈ damagedBlocks }
```

---

## 2023 Exam

### Question 1: Queue System (VDM Notation)
**Marks:** 3+3+4=10  
**CLO:** 3

#### Data Types and Free Data Type:
```
types Element = <Element>
```

#### State Schema:
```
State Queue
  queue: seq of Element
  SIZE: ℕ
  inv mk-Queue(q, s) == len q ≤ s
  init mk-Queue(q, s) == q = []
```

#### Operation Schemas:

**Enqueue:**
```
Enqueue(e?: Element)
  ext wr queue: seq of Element
  pre len queue < SIZE
  post queue' = queue ^ [e?]
```

**Dequeue:**
```
Dequeue() e!: Element
  ext wr queue: seq of Element
  pre queue ≠ []
  post queue' = tl queue ∧ e! = hd queue
```

**isFull:**
```
isFull() b!: Boolean
  ext rd queue: seq of Element
  pre true
  post b! = (len queue = SIZE)
```

**isEmpty:**
```
isEmpty() b!: Boolean
  ext rd queue: seq of Element
  pre true
  post b! = (queue = [])
```

### Question 2: University System (Z Notation)
**CLO:** 3, 4

*Same as Question 1 from 2022 Spring Exam*

### Question 3: Hotel Info Desk (VDM Notation)
**Marks:** 4+6=10  
**CLO:** 3

#### Data Types:
```
types Room = <Room>
```

#### State Schema:
```
State HotelInfoDesk
  occupied: ℕ
  vacant: ℕ
  TOTAL: ℕ
  inv mk-HotelInfoDesk(o, v, t) == o + v = t ∧ o ≥ 0 ∧ v ≥ 0
  init mk-HotelInfoDesk(o, v, t) == o = 0 ∧ v = t
```

#### Operation Schemas:

**RoomVacant:**
```
RoomVacant()
  ext wr occupied: ℕ
  wr vacant: ℕ
  pre occupied > 0
  post occupied' = occupied - 1
  post vacant' = vacant + 1
```

**RoomOccupied:**
```
RoomOccupied()
  ext wr occupied: ℕ
  wr vacant: ℕ
  pre vacant > 0
  post occupied' = occupied + 1
  post vacant' = vacant - 1
```

### Question 4: Airport System (Z Notation)
**CLO:** 3, 4

*Same as Question 2 from 2022 Exam*

### Question 5: Petri Net Analysis
**Marks:** 4+1+2+3=10  
**CLO:** 3, 4

**Note:** This question requires a Petri net diagram that was not provided in the original text. The general approach involves:
1. Generate reachability graph
2. Check boundedness
3. Identify issues
4. Suggest fixes (e.g., adding mutual exclusivity constraints)

---

## Key Concepts Covered

### Z Notation
- **State Schemas:** Define system state with invariants
- **Operation Schemas:** Define state transitions
- **Delta (Δ):** Indicates state change
- **Xi (Ξ):** Indicates no state change (read-only)
- **Input/Output:** `?` for input, `!` for output
- **Set Operations:** ℙ (power set), ∪ (union), ∩ (intersection), \ (difference)
- **Relations:** ↦ (total function), ↣ (partial function)

### VDM Notation
- **State:** `State` keyword with variables and invariants
- **Operations:** `Operation` keyword with pre/post conditions
- **External Variables:** `ext wr` (write), `ext rd` (read)
- **Initialization:** `init` keyword
- **Types:** `types` keyword for type declarations
- **Sequences:** `seq of` for sequence types
- **Sets:** `set of` for set types

### Common Patterns
1. **Resource Management:** Capacity limits, counting
2. **Set Operations:** Union (∪), intersection (∩), difference (\)
3. **Preconditions:** Input validation
4. **Postconditions:** State changes and outputs
5. **Invariants:** System constraints that must always hold

---

*This document contains comprehensive solutions to formal methods past papers and quizzes, covering Z notation and VDM specifications with proper syntax for each notation.*
