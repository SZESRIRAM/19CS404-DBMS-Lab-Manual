# ER Diagram Workshop – Submission Template

## Objective
To understand and apply ER modeling concepts by creating ER diagrams for real-world applications.

## Purpose
Gain hands-on experience in designing ER diagrams that represent database structure including entities, relationships, attributes, and constraints.

---

# Scenario A: City Fitness Club Management

**Business Context:**  
FlexiFit Gym wants a database to manage its members, trainers, and fitness programs.

**Requirements:**  
- Members register with name, membership type, and start date.  
- Each member can join multiple programs (Yoga, Zumba, Weight Training).  
- Trainers assigned to programs; a program may have multiple trainers.  
- Members may book personal training sessions with trainers.  
- Attendance recorded for each session.  
- Payments tracked for memberships and sessions.

### ER Diagram:
<img width="862" height="662" alt="image" src="https://github.com/user-attachments/assets/9a747c6b-a383-44f2-ae13-e36f96341d0e" />


### Entities and Attributes

| Entity | Attributes (PK, FK) | Notes |
|--------|--------------------|-------|
| Trainer | PK: trainer_id, name, specialization, phone_no | Stores trainer details |
| Program | PK: program_id, name, category | Stores fitness program details |
| Member | PK: member_id, name, email, member_type | Stores gym member details |
| Session | PK: session_id, FK: trainer_id, FK: member_id, session_type, session_time | Stores personal training session details |
| Payment | PK: payment_id, FK: member_id, payment_type | Stores membership and session payments |
| Attendance | PK: attendance_id, FK: session_id, status, date | Records attendance for sessions |

### Relationships and Constraints

| Relationship | Cardinality | Participation | Notes |
|--------------|-------------|---------------|-------|
| Trainer - Program (teaches) | M : N | Partial on both sides | A trainer can teach multiple programs, and a program can have multiple trainers |
| Member - Program (joins) | M : N | Partial on both sides | A member can join multiple programs, and a program can have multiple members |
| Member - Session (books) | 1 : M | Session is total | A member can book multiple training sessions |
| Trainer - Session (handles) | 1 : M | Session is total | A trainer can handle multiple sessions |
| Member - Payment (makes) | 1 : M | Payment is total | A member can make multiple payments |
| Session - Attendance (records) | 1 : 0..1 | Attendance is optional | Attendance is recorded for a session when applicable |

### Assumptions

- Each trainer, program, member, session, payment, and attendance record has a unique ID.
- A trainer can teach multiple programs, and each program can be taught by multiple trainers.
- A member can join multiple programs and book multiple personal training sessions.
- Each session is booked by one member and handled by one trainer.
- Payments are made by members for memberships or personal training sessions.
- Attendance records store the session date and status, such as Present or Absent.

---

# Scenario B: City Library Event & Book Lending System

**Business Context:**  
The Central Library wants to manage book lending and cultural events.

**Requirements:**  
- Members borrow books, with loan and return dates tracked.  
- Each book has title, author, and category.  
- Library organizes events; members can register.  
- Each event has one or more speakers/authors.  
- Rooms are booked for events and study.  
- Overdue fines apply for late returns.

### ER Diagram:
*Paste or attach your diagram here*  
<img width="1758" height="895" alt="image" src="https://github.com/user-attachments/assets/76f74e0f-f69b-4bdf-a507-da70cb79790a" />


### Entities and Attributes

| Entity | Attributes (PK, FK) | Notes |
|--------|--------------------|-------|
| Member | PK: Member_ID, Name | Stores library member details |
| Book | PK: Book_ID, Title, Author, Category | Stores book information |
| Loan | PK: Loan_ID, FK: Member_ID, FK: Book_ID, Loan_Date, Return_Date, Due_Date | Tracks book borrowing and returns |
| Event | PK: Event_ID, Name, Date | Stores library event details |
| Speaker | PK: Speaker_ID, Name | Stores speaker and author details |
| Event_Speaker | PK, FK: Event_ID; PK, FK: Speaker_ID | Connects events and speakers |
| Event_Registration | PK, FK: Member_ID; PK, FK: Event_ID | Tracks member event registrations |
| Room | PK: Room_ID, Room_Name, Capacity | Stores rooms for events and study |
| Room_Booking | PK: Booking_ID, FK: Room_ID, FK: Event_ID (nullable), Booking_Date, Start_Time, End_Time | Tracks event and study room bookings |
| Fine | PK: Fine_ID, FK: Loan_ID, Amount, Payment_Status | Tracks overdue fines |

### Relationships and Constraints

| Relationship | Cardinality | Participation | Notes |
|--------------|-------------|---------------|-------|
| Member - Loan | 1 : M | Loan is total | A member can borrow multiple books |
| Book - Loan | 1 : M | Loan is total | A book can have multiple loan records over time |
| Member - Event_Registration | 1 : M | Registration is total | A member can register for multiple events |
| Event - Event_Registration | 1 : M | Registration is total | An event can have multiple registered members |
| Event - Speaker | M : N | Partial on both sides | An event can have multiple speakers, and a speaker can attend multiple events |
| Event - Room_Booking | 1 : M | Room booking is total for event bookings | Events use booked rooms |
| Room - Room_Booking | 1 : M | Room booking is total | A room can have multiple bookings at different times |
| Loan - Fine | 1 : 0..1 | Fine is optional | A loan may generate a fine for an overdue return |

### Assumptions

- Each member, book, loan, event, speaker, room, and fine has a unique ID.
- Each loan belongs to one member and one book, and loan and return dates are recorded.
- Each book has a title, author, and category.
- Members can register for multiple events, and events can have multiple registered members.
- Each event has one or more speakers or authors.
- Rooms can be booked for events or individual study, and overlapping bookings for the same room are not allowed.
- Overdue fines apply when a book is returned after its due date.

---

# Scenario C: Restaurant Table Reservation & Ordering

**Business Context:**  
A popular restaurant wants to manage reservations, orders, and billing.

**Requirements:**  
- Customers can reserve tables or walk in.  
- Each reservation includes date, time, and number of guests.  
- Customers place food orders linked to reservations.  
- Each order contains multiple dishes; dishes belong to categories (starter, main, dessert).  
- Bills generated per reservation, including food and service charges.  
- Waiters assigned to serve reservations.

### ER Diagram:
<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/5515dd9a-02ec-4808-80c7-732bdd91c8ed" />

## Restaurant Management ER Diagram

### Entities and Attributes

| Entity | Attributes (PK, FK) | Notes |
|--------|--------------------|-------|
| Customer | PK: Customer_ID, Name | Stores customer details |
| Reservation | PK: Reservation_ID, FK: Customer_ID, FK: Waiter_ID, Name, Reservation_Date | Tracks table reservations |
| Waiter | PK: Waiter_ID, Name | Stores waiter details |
| Category | PK: Category_ID, Category_Name | Groups dishes |
| Dish | PK: Dish_ID, FK: Category_ID, Name, Price | Stores menu items |
| Order | PK: Order_ID, FK: Reservation_ID, FK: Waiter_ID | Orders placed against a reservation |
| Order_Item | PK, FK: Order_ID; PK, FK: Dish_ID; Quantity | Connects orders and dishes |
| Bill | PK: Bill_ID, FK: Order_ID, Amount | Final bill for an order |

### Relationships and Constraints

| Relationship | Cardinality | Participation | Notes |
|--------------|-------------|---------------|-------|
| Customer - Reservation | 1 : M | Reservation is total | A customer can make multiple reservations |
| Waiter - Reservation | 1 : M | Reservation is partial | A waiter handles multiple reservations |
| Reservation - Order | 1 : M | Order is total | A reservation can have multiple orders |
| Waiter - Order | 1 : M | Order is total | A waiter serves multiple orders |
| Category - Dish | 1 : M | Dish is total | Each dish belongs to one category |
| Order - Dish | M : N | Partial on both sides | Resolved through Order_Item |
| Order - Bill | 1 : 1 | Bill is total | Every order produces one bill |

### Assumptions

- Each entity has a unique ID.
- Each reservation belongs to one customer and is assigned to one waiter.
- Each dish belongs to one category and has a name and price.
- An order can include multiple dishes, each with a quantity.
- Each order generates one bill, calculated from Quantity × Price of its items.
---

## Instructions for Students

1. Complete **all three scenarios** (A, B, C).  
2. Identify entities, relationships, and attributes for each.  
3. Draw ER diagrams using **draw.io / diagrams.net** or hand-drawn & scanned.  
4. Fill in all tables and assumptions for each scenario.  
5. Export the completed Markdown (with diagrams) as **a single PDF**
