<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>FY26 Budget Expenditures</title>
    
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600&display=swap" rel="stylesheet">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Inter', sans-serif;
        }
        body {
            background-color: #f4f9f4;
            text-align: center;
            padding: 20px;
            overflow-x: hidden;
        }
        h1 {
            color: #2d6a4f;
            font-size: 2.2rem;
        }
        .nav-container {
            margin-bottom: 10px;
        }
        .nav-container select {
            padding: 5px;
            font-size: 1rem;
            border: 1px solid #2d6a4f;
            border-radius: 5px;
        }
        .table-container {
            width: 100%;
            max-height: 90vh;
            overflow-y: auto;
            background: white;
            border-radius: 8px;
            padding: 10px;
            box-shadow: 0px 4px 6px rgba(0, 0, 0, 0.1);
        }
        table {
            width: 100%;
            border-collapse: collapse;
            table-layout: fixed;
        }
        th, td {
            border: 1px solid #ddd;
            padding: 12px;
            text-align: left;
            white-space: nowrap;
        }
        th {
            background-color: #2d6a4f;
            color: white;
            position: sticky;
            top: 0;
            z-index: 10;
        }
        tr:nth-child(even) {
            background-color: #f1f8f1;
        }
        td:first-child {
            font-weight: bold;
            background-color: #d4edda;
        }
    </style>
</head>
<body>
    <h1>FY26 Budget Expenditures</h1>
    
    <div class="nav-container">
        <label for="departmentDropdown">Jump To:</label>
        <select id="departmentDropdown" onchange="jumpToDepartment()">
            <option value="">Select...</option>
        </select>
    </div>
    
    <div class="table-container">
        <table id="budgetTable">
            <thead>
                <tr id="tableHeader"></tr>
            </thead>
            <tbody>
                <tr><td colspan="100%" class="error">Loading budget data...</td></tr>
            </tbody>
        </table>
    </div>
    
    <script>
        document.addEventListener("DOMContentLoaded", function () {
            loadBudgetData();
        });

        async function loadBudgetData() {
            const csvUrl = "https://raw.githubusercontent.com/NBoudreauMA/FY26/main/docs/budget2.csv";
            try {
                const response = await fetch(csvUrl);
                if (!response.ok) throw new Error("Failed to load CSV file. Ensure the URL is correct.");
                const data = await response.text();
                populateTable(data);
            } catch (error) {
                document.querySelector("#budgetTable tbody").innerHTML = `<tr><td colspan="100%">${error.message}</td></tr>`;
            }
        }

        function populateTable(csvText) {
            const tableHeader = document.querySelector("#tableHeader");
            const tableBody = document.querySelector("#budgetTable tbody");
            const dropdown = document.querySelector("#departmentDropdown");
            const rows = csvText.trim().split("\n").map(row => row.split(","));
            
            tableHeader.innerHTML = rows[0].map(header => `<th>${header.trim()}</th>`).join("");
            let tableContent = "";
            let departments = new Set();
            
            rows.slice(1).forEach(row => {
                let department = row[0] ? row[0].trim() : "";
                if (department && !departments.has(department)) {
                    departments.add(department);
                    let option = document.createElement("option");
                    option.value = department.replace(/\s+/g, '');
                    option.textContent = department;
                    dropdown.appendChild(option);
                }
                tableContent += "<tr>" + row.map(cell => `<td>${cell.trim()}</td>`).join("") + "</tr>";
            });
            tableBody.innerHTML = tableContent;
        }
        
        function jumpToDepartment() {
            const dropdown = document.querySelector("#departmentDropdown");
            const selectedDept = dropdown.value;
            if (selectedDept) {
                document.getElementById(selectedDept)?.scrollIntoView({ behavior: "smooth" });
            }
        }
    </script>
</body>
</html>
