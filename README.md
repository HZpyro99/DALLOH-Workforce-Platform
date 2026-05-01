# 🏢 DALLOH: Workforce Time-Tracking & Productivity Platform

**Live Deployment:** [https://dalloh.dev.nimbus-solutions.tech/](https://dalloh.dev.nimbus-solutions.tech/)

> ⚠️ **Note:** The source code for this project is proprietary to Nimbus Solutions. This repository serves as a technical architecture case study detailing my specific contributions and feature integrations during my Software Development Internship (March 09, 2026 – April 17, 2026).

---

## 📌 Project Overview
DALLOH is a comprehensive, cloud-based workforce productivity platform designed to streamline employee time-tracking, task management, and profile administration. As a Software Developer Intern, my primary objective was to contribute to the MVP development by engineering the interactive calendar module, establishing backend service layers, and integrating real-time user clock-in data.

## 🛠️ Tech Stack & Architecture
*   **Backend Framework:** C#, ASP.NET MVC
*   **Database:** SQL Server, Entity Framework Core
*   **Frontend / UI:** JavaScript, HTML/CSS
*   **Third-Party Integrations:** FullCalendar API

---

## 🚀 Key Contributions & Feature Ownership

### 1. Interactive Calendar & CRUD Interface
*   Engineered the core interactive calendar module utilizing the FullCalendar API.
*   Established a full CRUD (Create, Read, Update, Delete) interface allowing managers and users to efficiently organize project timelines and assign daily tasks.

### 2. Visual Time-Tracking Integration
*   Integrated raw user clock-in and clock-out data directly into the calendar UI.
*   Transformed standard tabular timesheet data into an alternative, highly visual time-tracking mechanism for easier management oversight.

### 3. Secure Profile Management
*   Developed secure backend service layers for user profile management, seamlessly integrating the new module into the platform's established C#, ASP.NET MVC, and SQL Server architecture.

### 4. Codebase Integration & Architectural Troubleshooting
*   Navigated and integrated features into the platform's established enterprise data access layer (`Dalloh.Data` / Entity Framework Core).
*   Conducted code reviews and system debugging, identifying database integration conflicts for the internship team and proposing architectural workarounds to senior leadership.

---

## ⚙️ Engineering Challenges & Solutions

### The Challenge: Timezone Desynchronization & Non-Standard Data Structures
Integrating the interactive calendar module presented a significant data routing and parsing challenge between the FullCalendar UI and the SQL Server backend. 
*   **Timezone Mismatch:** The database strictly stored user clock-in and clock-out timestamps in UTC. Because the frontend lacked a mechanism to reverse this to the client's local time, the calendar UI displayed massive timing mismatches for users.
*   **Complex Data Payload:** The event data structure coming from the backend was non-standard. Instead of clean start/end timestamps, the data arrived in fragmented pairs flagged by integers: a `1` indicated a start time, and a `0` indicated an end time. FullCalendar could not natively parse or render this structure.

### The Solution: Backend Transformation Layer & Custom Parsing
To resolve the synchronization issues without compromising the integrity of the UTC database, I engineered a dedicated data transformation layer within the ASP.NET MVC backend.

1.  **Timezone Interception:** I implemented a backend utility to intercept the UTC timestamps pulled from the SQL Server. Before serializing the payload for the frontend, the utility mapped the UTC data directly to the user's local timezone (accurately applying the UTC+8 offset for local Philippine users), ensuring the UI rendered the exact local clock-in times.
2.  **Custom DTO (Data Transfer Object) Mapping:** Instead of forcing the frontend to decipher the `1` (start) and `0` (end) flags, I built a custom parsing logic layer in C#. This layer iterated through the fragmented database pairs, matched the corresponding `1` and `0` flags for a specific task, and combined them into a single, standardized JSON object with clear `start` and `end` DateTime properties that the FullCalendar API could seamlessly consume.

---

## 📸 System Showcase
<img width="1919" height="948" alt="image" src="https://github.com/user-attachments/assets/459bcd8b-040a-46dc-997f-d260e86369c0" />

<img width="1919" height="950" alt="image" src="https://github.com/user-attachments/assets/94b9b966-1780-43b5-954d-21b0af62a2fa" />

<img width="1915" height="942" alt="image" src="https://github.com/user-attachments/assets/0f9bca0e-27bc-4282-ab3e-7f815462a1c9" />

<img width="1919" height="953" alt="image" src="https://github.com/user-attachments/assets/a61505fb-3da2-4000-b7d9-fa390ae3ef81" />

<img width="1919" height="942" alt="image" src="https://github.com/user-attachments/assets/e1d26c1c-3a97-4413-b56c-04a28648410b" />
