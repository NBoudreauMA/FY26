<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>FY26 Budget Expenditures</title>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            padding: 20px;
            background-color: #f4f9f4;
        }
        h1 {
            color: #2d6a4f;
        }
        .nav-container {
            position: sticky;
            top: 0;
            background-color: #2d6a4f;
            padding: 10px;
            z-index: 1000;
            text-align: left;
        }
        .nav-container a {
            color: white;
            margin: 0 10px;
            text-decoration: none;
            font-weight: bold;
        }
        .table-container {
            width: 100%;
            overflow-x: auto;
            margin-top: 20px;
        }
        table {
            width: 100%;
            border-collapse: collapse;
            table-layout: fixed;
            white-space: nowrap;
        }
        th, td {
            border: 1px solid #ddd;
            padding: 8px;
            text-align: left;
        }
        th {
            background-color: #2d6a4f;
            color: white;
        }
        .scrollable {
            display: block;
            overflow-x: auto;
            max-width: 100%;
        }
        .dept-header {
            background-color: #d4edda;
            font-weight: bold;
            text-align: left;
            padding: 10px;
        }
    </style>
</head>
<body>

    <h1>FY26 Budget Expenditures</h1>
    
    <div class="nav-container" id="departmentNav"></div>
    
    <div class="table-container">
        <table id="budgetTable" class="scrollable">
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
            const navContainer = document.querySelector("#departmentNav");
            const rows = csvText.trim().split("\n").map(row => row.split(","));

            if (rows.length < 2) {
                tableBody.innerHTML = `<tr><td colspan="100%">No data available.</td></tr>`;
                return;
            }

            tableHeader.innerHTML = rows[0].map(header => `<th>${header.trim()}</th>`).join("");
            let tableContent = "";
            let departments = new Set();
            
            rows.slice(1).forEach(row => {
                let department = row[0].trim();
                if (department && !departments.has(department)) {
                    departments.add(department);
                    tableContent += `<tr id="${department.replace(/\s+/g, '')}" class="dept-header"><td colspan="100%">${department}</td></tr>`;
                }
                tableContent += "<tr>";
                row.forEach((cell, index) => {
                    let cellValue = cell.trim();
                    if (index === rows[0].length - 1) {
                        tableContent += `<td>${cellValue}%</td>`;
                    } else {
                        const numValue = parseFloat(cellValue);
                        tableContent += isNaN(numValue) ? `<td>${cellValue}</td>` : `<td>$${numValue.toLocaleString(undefined, {minimumFractionDigits: 2, maximumFractionDigits: 2})}</td>`;
                    }
                });
                tableContent += "</tr>";
            });
            tableBody.innerHTML = tableContent;

            let navLinks = "<strong style='color: white;'>Jump to: </strong>";
            departments.forEach(dept => {
                navLinks += `<a href="#${dept.replace(/\s+/g, '')}">${dept}</a>`;
            });
            navContainer.innerHTML = navLinks;
        }
    </script>

</body>
</html>
