# 🌍 Field Mapping System

A **Vue 3 + Vite + Leaflet.js** application for managing **field boundaries, farmer data, and role-based access control**.

---

## 🚀 Features

✅ **Interactive Map with Field Boundaries** – View & edit polygons for different roles.  
✅ **Role-Based Access Control (RBAC)** – Fine-grained permissions for different user types.  
✅ **Search & Filter Farmers and Fields** – Quickly locate information with an optimized search bar.  
✅ **Seamless Role Switching** – Instantly change between user roles for testing & validation.  
✅ **Sleek, Responsive UI** – Modern styling, smooth transitions, and intuitive navigation.  
✅ **Multiple Data Layers** – Overlay support for **satellite imagery & flagged error reports** (coming soon).

---

## 🎭 Role-Based Access Control

| **Role**                   | **Full Access** | **Dashboards** | **Edit Fields** | **View Only** | **Tracking** |
| -------------------------- | :-------------: | :------------: | :-------------: | :-----------: | :----------: |
| **Unlock Team**            |       ✅        |       ✅       |       ✅        |      ❌       |      ✅      |
| **Better Cotton**          |       ❌        |       ✅       |       ❌        |      ❌       |      ❌      |
| **Project Manager**        |       ❌        |       ✅       |       ❌        |      ✅       |      ✅      |
| **PU Manager**             |       ✅        |       ✅       |       ✅        |      ❌       |      ✅      |
| **Field Facilitator (FF)** |       ✅        |       ✅       |       ✅        |      ❌       |      ✅      |
| **Auditor**                |       ❌        |       ❌       |       ❌        |      ✅       |      ✅      |

---

## 🛠 Installation & Setup

### 🔹 Prerequisites

Ensure you have the following installed:

- **Node.js** (16+ recommended)
- **npm** (or **yarn**)
- **Vue 3** and **Vite**

### 🔹 Clone the Repository

```sh
git clone https://github.com/islas104/Field-Mapping-System.git
cd Field-Mapping-System
```

### 🔹 Install Dependencies

```sh
npm install
```

### 🔹 Run the Development Server

```sh
npm run dev
```

The app will be available at http://localhost:5173/.
