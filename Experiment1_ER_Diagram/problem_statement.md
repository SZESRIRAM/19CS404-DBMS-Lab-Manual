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
![ER Diagram](er_diagram_library.png)
### Entities and Attributes

| Entity | Attributes (PK, FK) | Notes |
|--------|--------------------|-------|
| Member | PK: Member_ID, Name, Email, Phone | Stores library member details |
| Book | PK: Book_ID, Title, Author, Category | Stores book details |
| Loan | PK: Loan_ID, FK: Member_ID, FK: Book_ID, Loan_Date, Due_Date, Return_Date | Tracks book borrowing and returns |
| Fine | PK: Fine_ID, FK: Loan_ID, Amount, Payment_Status | Tracks overdue fines |
| Event | PK: Event_ID, Event_Name, Event_Date, FK: Room_ID | Stores library events |
| Event_Registration | PK, FK: Member_ID; PK, FK: Event_ID, Registration_Date | Connects members and events |
| Speaker | PK: Speaker_ID, Name, Expertise | Stores speaker and author details |
| Event_Speaker | PK, FK: Event_ID; PK, FK: Speaker_ID | Connects events and speakers |
| Room | PK: Room_ID, Room_Name, Capacity | Stores library rooms |
| Room_Booking | PK: Booking_ID, FK: Room_ID, FK: Event_ID (nullable), Booking_Date, Start_Time, End_Time, Booking_Type | Tracks event and study room bookings |

### Relationships and Constraints

| Relationship | Cardinality | Participation | Notes |
|--------------|-------------|---------------|-------|
| Member - Loan | 1 : M | Loan is total | A member can borrow multiple books |
| Book - Loan | 1 : M | Loan is total | A book can have multiple loan records over time |
| Loan - Fine | 1 : 0..1 | Fine is optional | A loan may generate an overdue fine |
| Room - Event | 1 : M | Event is total | Each event takes place in one room |
| Member - Event_Registration | 1 : M | Registration is total | A member can register for multiple events |
| Event - Event_Registration | 1 : M | Registration is total | An event can have multiple registered members |
| Event - Speaker | M : N | Partial on both sides | An event can have multiple speakers |
| Room - Room_Booking | 1 : M | Booking is total | A room can have multiple bookings at different times |

### Assumptions

- Each member, book, event, speaker, and room has a unique ID.
- Each loan record refers to one member and one book, and a book can have multiple loan records over time.
- A fine is generated only when a book is returned late or an overdue fine becomes applicable.
- Each event is assigned one room and has one or more speakers.
- Members can register for multiple events, and events can have multiple registered members.
- Rooms can be booked for events or individual study, and overlapping bookings for the same room are not allowed.

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
*Paste or attach your diagram here*  
![ER Diagram](er_diagram_restaurant.png)

### Entities and Attributes

| Entity | Attributes (PK, FK) | Notes |
|--------|--------------------|-------|
| Customer | PK: Customer_ID, Name, Phone, Email | Stores customer details |
| Table | PK: Table_ID, Table_Number, Capacity | Stores restaurant table details |
| Reservation | PK: Reservation_ID, FK: Customer_ID, FK: Table_ID (nullable), Reservation_Date, Reservation_Time, Number_of_Guests, Reservation_Type | Tracks table reservations and walk-ins |
| Waiter | PK: Waiter_ID, Name, Phone | Stores waiter details |
| Reservation_Waiter | PK, FK: Reservation_ID; PK, FK: Waiter_ID | Assigns waiters to reservations |
| Food_Order | PK: Order_ID, FK: Reservation_ID, Order_Date, Order_Status | Stores orders linked to reservations |
| Dish | PK: Dish_ID, Dish_Name, FK: Category_ID, Price | Stores food menu items |
| Category | PK: Category_ID, Category_Name | Stores dish categories |
| Order_Item | PK, FK: Order_ID; PK, FK: Dish_ID, Quantity, Unit_Price | Connects orders and dishes |
| Bill | PK: Bill_ID, FK: Reservation_ID, Food_Amount, Service_Charge, Total_Amount, Payment_Status | Stores reservation billing details |

### Relationships and Constraints

| Relationship | Cardinality | Participation | Notes |
|--------------|-------------|---------------|-------|
| Customer - Reservation | 1 : M | Reservation is total | A customer can make multiple reservations |
| Table - Reservation | 1 : M | Reservation is partial | A table can be reserved at different times; walk-ins may not have a prior table reservation |
| Reservation - Food_Order | 1 : M | Food_Order is total | A reservation can have multiple food orders |
| Food_Order - Order_Item | 1 : M | Order_Item is total | Each order contains one or more dishes |
| Dish - Order_Item | 1 : M | Order_Item is total | A dish can appear in multiple orders |
| Category - Dish | 1 : M | Dish is total | Each dish belongs to one category |
| Reservation - Waiter | M : N | Partial on both sides | A reservation can be served by one or more waiters |
| Reservation - Bill | 1 : 0..1 | Bill is optional | A bill is generated for a reservation when required |

### Assumptions

- Each customer, table, reservation, waiter, order, dish, category, and bill has a unique ID.
- A reservation includes the date, time, and number of guests; walk-ins are recorded as reservations with type `Walk-in`.
- A table may be assigned to a reservation, but the table ID can be empty until a table is assigned.
- Each food order contains one or more dishes, and the quantity and unit price are recorded for each order item.
- Each dish belongs to one category, such as starter, main course, or dessert.
- Each reservation has at most one bill, which includes food charges and service charges. Overlapping table reservations are not allowed.
---

## Instructions for Students

1. Complete **all three scenarios** (A, B, C).  
2. Identify entities, relationships, and attributes for each.  
3. Draw ER diagrams using **draw.io / diagrams.net** or hand-drawn & scanned.  
4. Fill in all tables and assumptions for each scenario.  
5. Export the completed Markdown (with diagrams) as **a single PDF**
