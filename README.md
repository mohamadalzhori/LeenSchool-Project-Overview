# LeenSchool-Project-Overview
**LeenSchool** is a full-featured **multi-tenant** school management system built using **ASP.NET Core 8.0 MVC**, designed to streamline the academic, administrative, and communication workflows across schools. Built as a traditional web application with server-side rendering and Razor views, it is actively used in production, with complete per-school data isolation and supports PWA mobile usage with a focus on modularity and extensibility.

## 📋 Table of Contents

- [🔍 Overview](#-overview)
- [📖 Origin Story](#-origin-story)
- [📊 Project Scale & Impact](#-project-scale--impact)
- [💼 Professional Highlights](#-professional-highlights)
- [✨ Key Features](#-key-features)
- [🧠 Tech Stack](#-tech-stack)
- [🏗️ Architecture Overview](#️-architecture-overview)
- [🏫 Multi-Tenant by Design](#-multi-tenant-by-design)
- [🚀 Onboarding New Schools: Fast & Repeatable](#-onboarding-new-schools-fast--repeatable)
- [📝 Reflections & Takeaways](#-reflections--takeaways)

---

## 🔍 Overview

LeenSchool serves as a digital backbone for modern schools, offering dedicated portals for Admins, Teachers, and Students.

It enables full management of academic years, grades, subjects, schedules, payments, assessments, and more — all localized and mobile-optimized.

---

## 📖 Origin Story

LeenSchool was born from real-world pain points I observed while helping local schools manage operations with WordPress, Excel, and Google Sites. These tools worked — barely — but lacked structure, integration, and scalability.

By my third year of university, to address these limitations, I proposed a unified platform tailored to real-world school operations. The schools partnered with me directly, offering hands-on feedback and real-world testing. Within two weeks, the first version was live.

**Development Timeline & Evolution:**
- **June 2024**: Project kickoff with rapid prototyping
- **2 weeks**: First working version deployed
- **After 2 months**: Complete architectural rewrite for scalability and maintainability
- **Present**: Continuous enhancement with clean architecture principles

This project provided comprehensive software development experience across:
- **Frontend & Backend Development**
- **Database Design & Optimization**
- **User Experience & Interface Design**
- **DevOps & Deployment Pipelines**
- **Production Support & Maintenance**
- **Client Communication, Requirements Gathering, and Agile Development**

---

## 📊 Project Scale & Impact

- **Active Schools**: 3 production deployments
- **User Base**: 750+ students plus teachers and administrators
- **Data Volume**: Handling thousands of academic records, schedules, and assessments
- **Features**: 50+ core features across 3 role-based portals
- **Development**: 1+ year of continuous development and enhancement
- **Timeline**: From concept to production in under 3 months

---

## 💼 Professional Highlights

- **Full-Stack Ownership**: From database design to UI/UX implementation
- **Production-Ready**: Actively used by hundreds of users with production-level performance and business reliability
- **Scalable Architecture**: Multi-tenant design supporting growth
- **Modern Development**: Clean code, SOLID principles, automated deployments
- **User-Centric**: Built based on actual school workflow requirements
- **Maintenance**: Ongoing feature development and production support

---

## ✨ Key Features

### Admin Portal
- Comprehensive user management (Admins, Teachers, Students, Drivers, Logisticians)
- Manage Grades from KG2 up to Lebanese high school levels (ES2)
- Subjects management & assignment to Grades
- Define and manage:
  - Teacher schedules
  - Grade-level schedules
  - Tuition payments
  - Attendance tracking (with reporting)
- Review teacher lesson plans & performance assessments
- Manage teacher experience certificate requests (auto-generated & customizable)
- Points/rewards system for students
- Rich certificate designer and generator
- News management with system-wide notifications

### Teacher Portal
- Full subject management (lessons, homework, marks, attendance, points)
- Upload subject books automatically split into lessons
- Submit ratings and feedback
- Quiz builder (MCQ, True/False, Open-ended)
- Certificate requests, student success stories
- Access yearly school agenda

### Student Portal
- View subjects, lessons, homework, quizzes
- Track personal points and rewards
- Central dashboard for their academic progress

---

## 🧠 Tech Stack

| Layer        | Stack                                                                 |
|--------------|-----------------------------------------------------------------------|
| Backend      | ASP.NET Core 8.0 MVC (Server-side rendering)                         |
| DB           | PostgreSQL (EF Core, schema-per-tenant)                              |
| Auth         | ASP.NET Core Identity (Cookies-based)                                |
| PDF/Docs     | DinkToPdf, iTextSharp, iText7                                        |
| Email        | MailKit                                                               |
| Mapping      | AutoMapper                                                            |
| Logging      | Serilog                                                               |
| Frontend     | Razor Views with HTML, CSS, JavaScript                               |
| Localization | Multi-language support (Arabic, French, etc.)                        |
| Mobile       | PWA-enabled for student accessibility                                 |
| DevOps       | GitHub Actions → VPS (Apache + Systemd) deployment pipeline          |
| Hosting      | VPS (Ubuntu) with Apache + Systemd + PostgreSQL                      |

---

## 🏗️ Architecture Overview

LeenSchool follows **clean architecture principles** with **MVC (Model-View-Controller) pattern**, featuring:
- Server-side rendered Razor views for rich user interfaces
- Controller-based request handling and routing
- Repository pattern for data access abstraction
- IoC-based dependency injection
- Background job support for async tasks

This approach ensures fast initial loads, solid SEO, and a streamlined dev experience without the complexity of SPAs.

🧱 Key directories:
- `Controllers/` – MVC endpoints
- `Models/` – Entity and domain models
- `Services/` – Business logic
- `Repository/` – Data access abstraction
- `Views/` – Razor-based UI
- `Resources/` – Localization
- `Common/` – Cross-cutting concerns (logging, middlewares, validators, etc.)

---

## 🏫 Multi-Tenant by Design

LeenSchool supports **multi-tenant deployments**, isolating data by **PostgreSQL schemas**:

✅ Single database with isolated schemas per school                    
✅ Cost-effective infrastructure sharing                           
✅ Complete data isolation and security                             

---

## 🚀 Onboarding New Schools: Fast & Repeatable

Extremely streamlined - the entire process takes under an hour:

1. **Subdomain Setup**: Create custom subdomain (2 minutes)
2. **Database Setup**: Create new PostgreSQL schema (2 minutes)
3. **Deploy**: Run automated migrations via GitHub Actions (5 minutes)
4. **Configure**: Set school-specific settings and branding (10 minutes)
5. **Go Live**: VPS serves the new instance via Apache + Systemd (instant)

**Result**: A fully functional, customized school management system with branded URL ready for immediate use.

This approach keeps costs low while maintaining complete logical isolation between schools.

---

## 📝 Reflections & Takeaways

As much as LeenSchool is a technical achievement, it's also been a learning journey. Here are some key takeaways:

### ⚠️ Premature API Optimization Without Data
In the early stages, I made the endpoints too fine-grained based on assumptions rather than actual performance metrics. For instance:

Instead of using the standard student details endpoint and filtering data on the client side, I created multiple micro-endpoints like `/students/phone`, `/students/grade-id`, `/students/fullname`, etc.

The idea was to reduce bandwidth to accommodate mobile data constraints for most of the students. But I never validated this with any real measurements or profiling tools — it was speculative and lacked real data.

**The reality**: This added complexity and fragmented logic across the frontend/backend, for negligible real-world gain.

**What I'd do now**: Build for clarity first, measure second, then optimize only when needed. I'd use tools like Postman, browser dev tools, or application performance monitoring to make data-driven decisions before splitting endpoints.

### 📚 Other Key Learnings
- **User feedback trumps technical perfection**: Real user needs often differ from developer assumptions
- **Iterative deployment beats big-bang releases**: Smaller, frequent updates allowed faster feedback cycles
- **Documentation debt is real**: Features built without proper documentation became harder to maintain over time
