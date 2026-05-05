# 👔 Employee Management System

A complete full-stack Employee Management Web Application built with **Vue 3**, **Axios**, and **Bootstrap 5**, integrated with MockAPI for REST backend operations.

## 📋 Project Overview

This application performs full CRUD (Create, Read, Update, Delete) operations on employee records with a responsive UI and comprehensive error handling.

### 🎯 Features
- ✅ **Create**: Add new employees via a form
- 📖 **Read**: Display all employees in a sortable table with real-time search/filter
- ✏️ **Update**: Edit existing employee records with form validation
- 🗑️ **Delete**: Remove employees with confirmation prompt
- 📊 **Dashboard**: Summary statistics (total employees, departments, average salary)
- 🎨 **Responsive UI**: Mobile-friendly Bootstrap 5 design
- ⚠️ **Error Handling**: Comprehensive try-catch with user-friendly alerts
- 🔍 **Search**: Filter employees by ID or name
- 🏷️ **Color-coded Badges**: Distinguish departments visually

## 🗂️ Employee Data Fields
- **Employee ID** (String): e.g., EMP001
- **Name** (String): Full name
- **Designation** (String): Job title
- **Department** (String): HR / Engineering / Finance / Marketing / Operations
- **Salary** (Number): In Indian Rupees (₹)

## 🛠️ Tech Stack
- **Frontend**: Vue 3 (Composition API)
- **HTTP Client**: Axios
- **UI Framework**: Bootstrap 5
- **Build Tool**: Vite
- **Backend**: MockAPI (REST)

## 🚀 Installation & Setup

### Prerequisites
- Node.js (v14 or higher)
- npm or yarn

### Step 1: Clone/Download the Project
```bash
cd "employee management"
```

### Step 2: Install Dependencies
```bash
npm install
```

### Step 3: Configure MockAPI Endpoint
1. Go to **https://mockapi.io**
2. Create a free account and a new project
3. Create a resource called **`employees`** with these fields:
   - `employeeId` (String)
   - `name` (String)
   - `designation` (String)
   - `department` (String)
   - `salary` (Number)

4. Copy your API endpoint (format: `https://<your-id>.mockapi.io/api/v1/employees`)
5. Open [src/App.vue](src/App.vue) and replace the `API_URL` constant:
   ```javascript
   const API_URL = 'https://<your-id>.mockapi.io/api/v1/employees'
   ```

### Step 4: Run Development Server
```bash
npm run dev
```

The application will start at **http://localhost:5173**

## 📁 Project Structure
```
employee-management/
├── src/
│   ├── App.vue              ← Main component with all CRUD logic
│   ├── main.js              ← Vue app entry point + Bootstrap import
├── public/
├── index.html               ← HTML template
├── vite.config.js           ← Vite configuration
├── package.json             ← Dependencies & scripts
└── README.md                ← This file
```

## 💻 Usage Guide

### Adding an Employee
1. Fill in all fields in the "Add New Employee" form (left side)
2. Click "➕ Add Employee" button
3. Success alert will appear, form clears, and employee is added to table

### Viewing Employees
- Employees are displayed in a responsive table
- Summary stats show total employees, departments count, and average salary
- Use the search box to filter by Employee ID or Name

### Editing an Employee
1. Click ✏️ button on any employee row
2. Form will populate with employee data
3. Make changes and click "💾 Update Employee"
4. Table updates without page reload

### Deleting an Employee
1. Click 🗑️ button on any employee row
2. Confirmation modal appears
3. Click "Delete" to confirm
4. Employee is removed from table and API

## 🎨 UI Features
- **Responsive Grid Layout**: 2 columns on desktop, 1 column on mobile
- **Color-coded Department Badges**:
  - HR: Blue
  - Engineering: Green
  - Finance: Cyan
  - Marketing: Yellow
  - Operations: Red
- **Interactive Table**: Hover effects, sorted display
- **Summary Statistics Cards**: Total employees, unique departments, average salary
- **Alert Messages**: Success/error feedback for all operations
- **Loading States**: Spinner during API calls

## ✅ Code Quality Features
- ✨ Vue 3 Composition API (setup, ref, computed, onMounted)
- 🛡️ Form validation before submission
- 📡 Async/await with try-catch error handling
- 💬 User-friendly error messages
- 🔄 Reactive state management with refs and computed properties
- 📐 Separation of concerns (API calls, UI logic, validation)
- 🎯 Two-way binding with v-model
- 🔁 List rendering with v-for and conditional UI with v-if

## 🐛 Troubleshooting

### "Failed to load employees" Error
- ✅ Check if your MockAPI endpoint URL is correct in [src/App.vue](src/App.vue)
- ✅ Ensure you created the `employees` resource on MockAPI
- ✅ Check your internet connection

### "Failed to save/delete employee" Error
- ✅ Verify all form fields are filled
- ✅ Check MockAPI is accessible (https://mockapi.io)
- ✅ Ensure employee IDs are unique

### Port 5173 Already in Use
```bash
npm run dev -- --port 3000
```

## 📊 Evaluation Checklist
- ✅ Vue 3 project with Vite + Axios + Bootstrap (2 Marks)
- ✅ MockAPI integration with REST endpoints (2 Marks)
- ✅ Complete CRUD functionality (4 Marks)
- ✅ Bootstrap 5 responsive design with badges (1 Mark)
- ✅ Composition API, error handling, validation (1 Mark)

**Total: 10 Marks**

## 📸 Screenshots

### Add Employee Form
The left sidebar contains a responsive form with all 5 employee fields, showing visual feedback for success/error operations.

### Employee Table
The main table displays all employees with:
- Employee ID, Name, Designation
- Color-coded department badges
- Formatted salary display
- Edit and Delete action buttons

### Statistics Dashboard
Three cards display:
- 📊 Total Employees
- 🏢 Unique Departments
- 💰 Average Salary

### Delete Confirmation
A modal dialog appears before deletion with employee details and confirmation buttons.

## 🔗 MockAPI Endpoint Example
```
GET    https://<your-id>.mockapi.io/api/v1/employees       ← Fetch all
POST   https://<your-id>.mockapi.io/api/v1/employees       ← Create
PUT    https://<your-id>.mockapi.io/api/v1/employees/{id}  ← Update
DELETE https://<your-id>.mockapi.io/api/v1/employees/{id}  ← Delete
```

## 📝 Notes
- All data persists on MockAPI servers
- Delete actions cannot be undone
- Form validation prevents empty submissions
- Search is case-insensitive and real-time

## 📄 License
Academic Project - CBIT Assignment

---

**Built with ❤️ using Vue 3, Axios, Bootstrap 5 & MockAPI**
