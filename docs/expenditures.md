<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>FY26 Budget Expenditures</title>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <style>
        body {
            font-family: 'Arial', sans-serif;
            background-color: #f4f9f4;
            margin: 0;
            padding: 0;
            text-align: center;
        }
        h1 {
            color: #2d6a4f;
            margin-top: 20px;
        }
        .nav-container {
            position: sticky;
            top: 0;
            background-color: #2d6a4f;
            padding: 10px;
            z-index: 1000;
            display: flex;
            justify-content: flex-end;
            align-items: center;
        }
        .nav-container label {
            color: white;
            font-weight: bold;
            margin-right: 10px;
        }
        .nav-container select {
            background-color: white;
            color: #2d6a4f;
            font-weight: bold;
            border: 1px solid #2d6a4f;
            padding: 5px;
            border-radius: 5px;
            cursor: pointer;
            font-size: 14px;
        }
        .table-container {
            width: 95%;
            margin: auto;
            max-height: 80vh;
            overflow-y: auto; /* Vertical scrolling only */
            background: white;
            border: 1px solid #ddd;
        }
        table {
            width: 100%;
            border-collapse: collapse;
            table-layout: fixed; /* Keeps spacing correct */
        }
        th, td {
            border: 1px solid #ddd;
            padding: 8px;
            text-align: left;
            white-space: nowrap;
            overflow: hidden;
            text-overflow: ellipsis;
        }
        th {
            background-color: #2d6a4f;
            color: white;
            position: sticky;
            top: 0;
            z-index: 100;
        }
        td {
            min-width: 80px; /* Keeps columns evenly spaced */
        }
        .department-header {
            background-color: #d4edda;
            font-weight: bold;
            text-align: left;
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
                <tr>
                    <td colspan="100%" class="error">Loading budget data...</td>
                </tr>
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
                    tableContent += `<tr id="${department.replace(/\s+/g, '')}" class="department-header"><td colspan="${rows[0].length}">${department}</td></tr>`;
                    let option = document.createElement("option");
                    option.value = department.replace(/\s+/g, '');
                    option.textContent = department;
                    dropdown.appendChild(option);
                }
                tableContent += "<tr>";
                row.forEach((cell, index) => {
                    let cellValue = cell.trim();
                    const isPercentageColumn = rows[0][index].toLowerCase().includes("change");
                    
                    if (isPercentageColumn && !isNaN(parseFloat(cellValue))) {
                        tableContent += `<td>${parseFloat(cellValue).toFixed(1)}%</td>`;
                    } else if (!isNaN(parseFloat(cellValue))) {
                        tableContent += `<td>$${parseFloat(cellValue).toLocaleString(undefined, {minimumFractionDigits: 2, maximumFractionDigits: 2})}</td>`;
                    } else {
                        tableContent += `<td>${cellValue}</td>`;
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
