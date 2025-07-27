# Employee-management
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Employee Management App</title>
  <style>
    body {
      font-family: 'Segoe UI', sans-serif;
      background: linear-gradient(to right, #74ebd5, #9face6);
      margin: 0;
      padding: 0;
    }

    nav {
      background-color: #2c3e50;
      padding: 1rem;
      display: flex;
      justify-content: center;
      gap: 20px;
    }

    nav a {
      color: white;
      text-decoration: none;
      font-weight: bold;
    }

    nav a:hover {
      text-decoration: underline;
    }

    .container {
      max-width: 800px;
      margin: 2rem auto;
      padding: 2rem;
      background-color: white;
      border-radius: 12px;
      box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
    }

    form input, form button {
      display: block;
      width: 100%;
      padding: 10px;
      margin: 10px 0;
      border-radius: 6px;
      border: 1px solid #ccc;
      font-size: 16px;
    }

    form button {
      background-color: #3498db;
      color: white;
      border: none;
      cursor: pointer;
    }

    form button:hover {
      background-color: #2980b9;
    }

    table {
      width: 100%;
      border-collapse: collapse;
    }

    th, td {
      padding: 12px;
      text-align: left;
      border-bottom: 1px solid #ddd;
    }

    th {
      background-color: #2980b9;
      color: white;
    }
  </style>
</head>
<body>
  <nav>
    <a href="#" onclick="showPage('dashboard')">Dashboard</a>
    <a href="#" onclick="showPage('add')">Add Employee</a>
    <a href="#" onclick="showPage('view')">View Employees</a>
  </nav>

  <!-- Dashboard Page -->
  <div class="container" id="dashboardPage">
    <h1>Welcome to Employee Management System</h1>
    <p>Use the navigation above to manage your employees.</p>
  </div>

  <!-- Add Employee Page -->
  <div class="container" id="addPage" style="display:none">
    <h2>Add New Employee</h2>
    <form id="addForm">
      <input type="text" id="name" placeholder="Name" required />
      <input type="text" id="position" placeholder="Position" required />
      <input type="email" id="email" placeholder="Email" required />
      <input type="text" id="location" placeholder="Location" required />
      <button type="submit">Save</button>
    </form>
  </div>

  <!-- View Employees Page -->
  <div class="container" id="viewPage" style="display:none">
    <h2>Employee List</h2>
    <table>
      <thead>
        <tr>
          <th>Name</th>
          <th>Position</th>
          <th>Email</th>
          <th>Location</th>
        </tr>
      </thead>
      <tbody id="employeeList"></tbody>
    </table>
  </div>

  <script>
    function showPage(pageId) {
      document.getElementById("dashboardPage").style.display = "none";
      document.getElementById("addPage").style.display = "none";
      document.getElementById("viewPage").style.display = "none";

      if (pageId === "dashboard") {
        document.getElementById("dashboardPage").style.display = "block";
      } else if (pageId === "add") {
        document.getElementById("addPage").style.display = "block";
      } else if (pageId === "view") {
        document.getElementById("viewPage").style.display = "block";
        displayEmployees(); // refresh list
      }
    }

    document.getElementById("addForm").addEventListener("submit", function(e) {
      e.preventDefault();

      const name = document.getElementById("name").value;
      const position = document.getElementById("position").value;
      const email = document.getElementById("email").value;
      const location = document.getElementById("location").value;

      const employee = { name, position, email, location };

      let employees = JSON.parse(localStorage.getItem("employees")) || [];
      employees.push(employee);
      localStorage.setItem("employees", JSON.stringify(employees));

      alert("Employee added successfully!");
      this.reset();
      showPage("view");
    });

    function displayEmployees() {
      const employeeList = document.getElementById("employeeList");
      employeeList.innerHTML = "";

      const employees = JSON.parse(localStorage.getItem("employees")) || [];

      employees.forEach(emp => {
        const row = document.createElement("tr");
        row.innerHTML = `
          <td>${emp.name}</td>
          <td>${emp.position}</td>
          <td>${emp.email}</td>
          <td>${emp.location}</td>
        `;
        employeeList.appendChild(row);
      });
    }

    document.addEventListener("DOMContentLoaded", () => {
      showPage("dashboard");
    });
  </script>
</body>
</html>
