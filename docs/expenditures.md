<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>FY26 Budget Expenditures</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            background-color: #f5f5f5;
            margin: 0;
            padding: 20px;
        }
        h1 {
            color: #5a2d82;
        }
        table {
            width: 90%;
            margin: auto;
            border-collapse: collapse;
            background-color: white;
        }
        thead {
            position: sticky;
            top: 0;
            background-color: #5a2d82;
            color: white;
            z-index: 100;
        }
        th, td {
            border: 1px solid #ddd;
            padding: 8px;
            text-align: left;
            white-space: nowrap;
        }
        th {
            background-color: #5a2d82;
            color: white;
            font-weight: bold;
        }
        tr:nth-child(even) {
            background-color: #f2f2f2;
        }
        .container {
            max-width: 1200px;
            margin: auto;
            overflow-x: auto;
        }
    </style>
</head>
<body>
    <h1><a href="index.html" style="text-decoration: none; color: #5a2d82;">FY26</a></h1>
    <h2 style="color: #5a2d82;">FY26 Budget Expenditures</h2>
    <p>This page provides an overview of the expenditures for the Town of Hubbardston.</p>
    
    <div class="container">
        <table id="budget-table">
            <thead>
                <tr>
                    <th>Department</th>
                    <th>Category</th>
                    <th>FY24</th>
                    <th>FY25 Request</th>
                    <th>FY25</th>
                    <th>FY26 Dept</th>
                    <th>FY26 Admin</th>
                    <th>Change ($)</th>
                    <th>Change (%)</th>
                </tr>
            </thead>
            <tbody>
                <!-- Data will be inserted here -->
            </tbody>
        </table>
    </div>

    <script>
        document.addEventListener("DOMContentLoaded", function () {
            fetch("https://raw.githubusercontent.com/NBoudreauMA/FY26/main/docs/assets/budget.csv")
                .then(response => response.text())
                .then(data => {
                    let rows = data.split("\n").map(row => row.split(","));
                    let tbody = document.querySelector("#budget-table tbody");

                    rows.forEach((row, index) => {
                        if (row.length > 1 && row.some(cell => cell.trim() !== "")) {
                            let tr = document.createElement("tr");
                            row.forEach(cell => {
                                let td = document.createElement("td");
                                td.textContent = cell.replace(/"/g, "").trim(); // Remove extra quotes and spaces
                                tr.appendChild(td);
                            });
                            tbody.appendChild(tr);
                        }
                    });
                })
                .catch(error => {
                    console.error("Error loading CSV data:", error);
                    let tbody = document.querySelector("#budget-table tbody");
                    tbody.innerHTML = `<tr><td colspan="9" style="color: red; text-align: center;">Error loading data</td></tr>`;
                });
        });
    </script>
</body>
</html>
