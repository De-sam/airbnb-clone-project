## Team Roles

This project is powered by a multidisciplinary software development team. Each role plays a critical part in ensuring smooth execution and delivery.

### 🧠 Business Analyst (BA)
- **Responsibilities:** Acts as a bridge between business needs and technical solutions.
- **Key Tasks:** Gathers requirements, analyzes business processes, and translates them into functional specifications for the dev team.

### 🧭 Product Owner (PO)
- **Responsibilities:** Owns the product vision and strategy.
- **Key Tasks:** Maintains the product backlog, prioritizes features, aligns deliverables with business goals, and ensures the final product meets customer expectations.

### 🧩 Project Manager (PM)
- **Responsibilities:** Oversees the planning and execution of the project.
- **Key Tasks:** Coordinates the team, manages timelines and resources, ensures delivery within scope and budget, and removes blockers.

### 🎨 UI/UX Designer
- **Responsibilities:** Designs user-friendly interfaces and intuitive user journeys.
- **Key Tasks:** Creates wireframes, prototypes, and final UI designs; conducts user research; ensures visual and functional consistency.

### 🏗️ Software Architect
- **Responsibilities:** Defines the software’s high-level structure and design.
- **Key Tasks:** Chooses tech stacks, designs scalable architecture, sets coding standards, and oversees technical decisions.

### 👨‍💻 Software Developer
- **Responsibilities:** Implements and maintains the product’s functionality.
- **Key Tasks:**
  - **Front-end:** Develops responsive interfaces and client-side logic.
  - **Back-end:** Builds APIs, handles data logic, and manages server-side components.
  - **Full-stack:** Handles both front-end and back-end development.

### 🧪 Quality Assurance (QA) Engineer
- **Responsibilities:** Validates that the software meets both functional and non-functional requirements.
- **Key Tasks:** Writes test cases, performs manual testing, logs bugs, and ensures consistent quality across releases.

### 🤖 Test Automation Engineer
- **Responsibilities:** Automates repetitive testing tasks to improve efficiency.
- **Key Tasks:** Builds test scripts, maintains test automation frameworks, and ensures reliable, continuous quality checks.

### ⚙️ DevOps Engineer
- **Responsibilities:** Enables smooth collaboration between development and operations.
- **Key Tasks:** Builds CI/CD pipelines, manages infrastructure, automates deployments, and ensures system reliability and scalability.

## 🛠️ Technology Stack

This project leverages a powerful set of technologies to build a robust, scalable, and flexible backend system, suitable for managing users, properties, bookings, and payments.

### ⚙️ Django
A high-level Python web framework that promotes rapid development and clean, pragmatic design.  
**Used for:** Building the core backend logic and serving REST and GraphQL APIs.

### 📦 Django REST Framework (DRF)
A powerful toolkit built on top of Django for creating Web APIs.  
**Used for:** Managing RESTful endpoints to handle CRUD operations for users, properties, bookings, and payments.

### 🐘 PostgreSQL
An advanced, open-source relational database system known for reliability and feature robustness.  
**Used for:** Storing all backend data including users, property listings, bookings, reviews, and payment records.

### 🔍 GraphQL
A query language and runtime for APIs that enables clients to request only the data they need.  
**Used for:** Providing flexible and efficient data querying as an alternative to REST.

### 🕒 Celery
A distributed task queue system.  
**Used for:** Handling background tasks such as sending emails, processing payments, and asynchronous booking confirmations.

### ⚡ Redis
An in-memory data structure store.  
**Used for:** Caching, session management, and as a message broker for Celery to boost performance and reduce DB load.

### 🐳 Docker
A containerization platform.  
**Used for:** Creating reproducible development environments and streamlining deployment across machines.

### 🔁 CI/CD Pipelines
Automated tools and scripts for Continuous Integration and Continuous Deployment.  
**Used for:** Automatically testing and deploying updates to ensure stability and reduce manual overhead.

## 🗃️ Database Design

The backend system is designed around a relational database structure with clear relationships between key entities. Below are the core models and how they interact.

### 👤 Users
Represents people using the platform—either as guests or hosts.

**Key Fields:**
- `id`: Unique identifier
- `username`: Unique username
- `email`: User’s email address
- `password`: Hashed password
- `is_host`: Boolean to distinguish between guest and host

**Relationships:**
- A user can **own multiple properties**
- A user can **make multiple bookings**
- A user can **write multiple reviews**

---

### 🏠 Properties
Represents listings available for booking.

**Key Fields:**
- `id`: Unique identifier
- `owner_id`: Foreign key to the user who owns the property
- `title`: Property title or name
- `description`: Detailed description
- `location`: Address or city of the property

**Relationships:**
- A property **belongs to a user (host)**
- A property can have **many bookings**
- A property can have **many reviews**

---

### 📅 Bookings
Represents reservations made by users.

**Key Fields:**
- `id`: Unique identifier
- `property_id`: Foreign key to the booked property
- `user_id`: Foreign key to the user who made the booking
- `start_date`: Check-in date
- `end_date`: Check-out date

**Relationships:**
- A booking **belongs to a user (guest)**
- A booking **belongs to a property**
- A booking **has one payment**

---

### 💳 Payments
Represents transaction records for bookings.

**Key Fields:**
- `id`: Unique identifier
- `booking_id`: Foreign key to the booking
- `amount`: Payment amount
- `status`: Payment status (e.g., paid, pending, failed)
- `timestamp`: Date and time of payment

**Relationships:**
- A payment **belongs to one booking**
- A booking **has one payment**

---

### 📝 Reviews
Represents feedback left by users after a stay.

**Key Fields:**
- `id`: Unique identifier
- `user_id`: Foreign key to the reviewer
- `property_id`: Foreign key to the reviewed property
- `rating`: Numeric score
- `comment`: Review text

**Relationships:**
- A review **belongs to a user**
- A review **belongs to a property**

---

### 🔗 Entity Relationship Summary
- A **User** can own many **Properties**
- A **User** can book many **Properties** (via **Bookings**)
- A **User** can write many **Reviews**
- A **Property** can have many **Bookings** and **Reviews**
- Each **Booking** is tied to one **User**, one **Property**, and one **Payment**
