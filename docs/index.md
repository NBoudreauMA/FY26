<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>FY26 Budget Expenditures</title>
    
    <!-- Google Fonts & Styling -->
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
        }
        h1 {
            color: #2d6a4f;
            font-size: 2.2rem;
        }
        .nav-container {
            display: flex;
            justify-content: flex-end;
            background-color: #2d6a4f;
            padding: 10px;
            border-radius: 8px;
            margin-bottom: 10px;
        }
        .nav-container select {
            background-color: white;
            color: #2d6a4f;
            font-weight: bold;
            border: 1px solid #2d6a4f;
            padding: 5px;
            border-radius: 5px;
            cursor: pointer;
        }
        .table-container {
            width: 100%;
            max-height: 75vh;
            overflow-y: auto;
            background: white;
            border-radius: 8px;
            padding: 10px;
            box-shadow: 0px 4px 6px rgba(0, 0, 0, 0.1);
        }
        table {
            width: 100%;
            border-collapse: collapse;
        }
        th, td {
            border: 1px solid #ddd;
            padding: 10px;
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
        tr:hover {
            background-color: #f1f8f1;
        }
    </style>
</head>
<body>
    <h1>FY26 Budget Expenditures</h1>
    
    <div class="nav-container">
        <label for="departmentDropdown" style="color: white; font-weight: bold;">Jump To:</label>
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
                    tableContent += `<tr id="${department.replace(/\s+/g, '')}" style="background-color:#d4edda; font-weight:bold;"><td colspan="100%">${department}</td></tr>`;
                    let option = document.createElement("option");
                    option.value = department.replace(/\s+/g, '');
                    option.textContent = department;
                    dropdown.appendChild(option);
                }
                tableContent += "<tr>";
                row.forEach((cell, index) => {
                    let cellValue = cell.trim();
                    if (index === rows[0].length - 1 && !isNaN(parseFloat(cellValue))) {
                        tableContent += `<td>${parseFloat(cellValue).toFixed(1)}%</td>`;
                    } else {
                        const numValue = parseFloat(cellValue);
                        tableContent += isNaN(numValue) ? `<td>${cellValue}</td>` : `<td>$${numValue.toLocaleString(undefined, {minimumFractionDigits: 2, maximumFractionDigits: 2})}</td>`;
                    }
                });
                tableContent += "</tr>";
            });
            tableBody.innerHTML = tableContent;
        }
        
        function jumpToDepartment() {
            const dropdown = document.querySelector("#departmentDropdown");
            const selectedDept = dropdown.value;
            if (selectedDept) {
                document.getElementById(selectedDept).scrollIntoView({ behavior: "smooth" });
            }
        }
    </script>
</body>
</html>
