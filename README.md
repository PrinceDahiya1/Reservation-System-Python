# TransitLink: Bus Reservation Engine

![Language](https://img.shields.io/badge/Language-Python_3-blue)
![Database](https://img.shields.io/badge/Database-MySQL-orange)
![Status](https://img.shields.io/badge/Status-Stable_(v1.0)-success)

**TransitLink** is a CLI-based transactional reservation system designed to manage bus e-ticketing operations. It bridges a **Python** frontend with a **MySQL** backend to handle high-frequency CRUD operations, seat availability tracking, and dynamic billing generation.

---

### 🚀 Key Features

* **Transactional Reservation Logic:** Implements atomic updates to ensure seat availability is synchronized instantly when a ticket is booked or cancelled.
* **Tiered Seating Architecture:** Supports dynamic class systems (**Regular** vs **Premium**) with distinct pricing models and availability tracking per bus.
* **Automated Billing:** Generates CLI-based invoices combining passenger details, route information, and calculated fares.
* **Data Seeding Module:** Includes a `GenerateGenericData.py` script to populate the database with thousands of realistic synthetic records for stress testing.
* **Formatted Reporting:** Utilizes `tabulate` to render complex SQL queries into human-readable grids.

---

### 🛠️ Technical Architecture

The system relies on a relational database schema to maintain data integrity.

**1. The Database (`project` schema)**
* **`buses` Table:** Acts as the inventory master. Stores `Bus_No`, `Destination`, `Departure_Time`, and manages real-time `Available_Seats`.
* **`seats` Table:** Acts as the transaction ledger. Stores individual `Ticket_No`, passenger `Name`, and links back to the specific bus via Foreign Key.

**2. The Logic (`FINAL DRAFT.py`)**
* **Connection Layer:** Uses `mysql.connector` to establish a persistent link to the local SQL server.
* **Business Layer:** Python functions handle input validation, seat allocation algorithms, and price calculation before committing changes to the DB.

---

### 💻 Installation & Setup

1.  **Clone the Repository**
    ```bash
    git clone https://github.com/PrinceDahiya1/transit-link.git
    ```

2.  **Configure the Database**
    * Ensure MySQL Server 8.0+ is installed.
    * Run the provided SQL dump to create the schema:
    ```bash
    mysql -u root -p project < MyProject.sql
    ```

3.  **Install Dependencies**
    ```bash
    pip install mysql-connector-python tabulate
    ```

4.  **Run the System**
    ```bash
    python "FINAL DRAFT.py"
    ```

---

### 📂 File Structure

| File | Description |
| :--- | :--- |
| `FINAL DRAFT.py` | The main application entry point containing the Menu and Logic. |
| `GenerateGenericData.py` | A utility script that uses randomization to seed the DB with test users/buses. |
| `MyProject.sql` | The SQL Dump file containing the schema structure and initial data. |
| `Login(Discontinued).py` | Legacy authentication module (deprecated). |

---

### 🔮 Future Roadmap
* [ ] **GUI Implementation:** Migrating from CLI to a Tkinter or PyQt5 interface.
* [ ] **Real-Time API:** Fetching live bus data from external transit APIs.
* [ ] **ORM Integration:** Refactoring raw SQL queries to use SQLAlchemy for better maintainability.
