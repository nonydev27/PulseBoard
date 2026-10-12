# ⚡ PulseBoard — Real-Time Role-Aware Project Tracker

PulseBoard is a multi-user, full-stack project and sprint management application built to demonstrate production-grade **Authentication**, **Role-Based Access Control (RBAC)**, **Real-Time WebSocket Synchronization**, and **Centralized Error & Notification UX**.

![Next.js](https://img.shields.io/badge/Next.js-15-black?style=flat-square&logo=next.js)
![TypeScript](https://img.shields.io/badge/TypeScript-5.0-blue?style=flat-square&logo=typescript)
![Supabase](https://img.shields.io/badge/Supabase-Auth%20%7C%20RLS%20%7C%20Realtime-3ECF8E?style=flat-square&logo=supabase)
![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-38B2AC?style=flat-square&logo=tailwind-css)

---

## ✨ Core Architecture & Features

### 1. 🔐 Full-Stack Auth & Session Refresh Strategy
- Powered by **Supabase Auth (`@supabase/ssr`)** with HTTP-only cookies.
- **Next.js Middleware** intercepts every request to validate and silently refresh expired JWT sessions before rendering server components.
- Automatic route protection redirecting unauthenticated users away from `/dashboard/*`.

### 2. 🛡️ Role-Based Access Control (RBAC)
Permissions are strictly enforced at both the **UI Component Layer** (via a custom `<RoleGate />` wrapper) and the **Database Layer** via PostgreSQL **Row-Level Security (RLS)**:

| Feature / Action | Admin | Project Lead | Member |
| :--- | :---: | :---: | :---: |
| Manage Workspace & User Roles | ✅ | ❌ | ❌ |
| Create & Archive Projects / Sprints | ✅ | ✅ | ❌ |
| Assign Tasks & Set Priorities | ✅ | ✅ | ❌ |
| Update Task Status (`Todo` → `Done`) | ✅ | ✅ | ✅ (Own/Assigned) |
| Post Real-Time Comments | ✅ | ✅ | ✅ |

### 3. ⚡ Real-Time WebSocket Subscriptions
- Uses **Supabase Realtime (`postgres_changes`)** to broadcast `INSERT`, `UPDATE`, and `DELETE` events on the `tasks` and `notifications` tables.
- Moving a task card or updating a role reflects across all connected browsers in under 100ms without page reloads.

### 4. 🔔 System Notifications & Toast Feeds
- **Live Notification Center:** Slide-over drawer and navbar badge tracking unread system events (task assignments, role changes, status updates).
- **Instant Toast Alerts:** Powered by `sonner`, converting incoming WebSocket payloads into interactive toast popups.

### 5. 🚨 Centralized Error-Handling & Toast UX
- Unified `withErrorHandling()` utility and global React Error Boundaries that intercept Supabase, PostgreSQL RLS (`42501`), and network errors.
- Automatically translates raw database error codes into human-readable, actionable toast alerts.

---

## 🛠️ Tech Stack

- **Frontend:** Next.js (App Router), TypeScript, Tailwind CSS, Lucide Icons
- **Backend & Database:** Supabase (PostgreSQL, Row-Level Security, Realtime Channels, Auth)
- **State & Notifications:** Sonner (Toast UX), React Context / Custom Realtime Hooks

---

## 🚀 Getting Started

### 1. Clone the repository
```bash
git clone ...
cd pulseboard-rbac
npm install
