<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Budget Expenditures</title>
    <link rel="stylesheet" href="assets/css/style.css">
    <style>
        table {
            width: 100%;
            border-collapse: collapse;
        }
        th, td {
            border: 1px solid black;
            padding: 8px;
            text-align: left;
        }
        th {
            background-color: #f2f2f2;
        }
    </style>
</head>
<body>

    <h1>Budget Expenditures</h1>
    <p>This page provides an overview of the expenditures for the Town of Hubbardston.</p>

    <table id="expendituresTable">
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

    <script>
        document.addEventListener("DOMContentLoaded", function() {
            fetch('https://raw.githubusercontent.com/NBoudreauMA/FY26/main/docs/assets/budget.csv')
            .then(response => response.text())
            .then(csv => {
                let rows = csv.trim().split("\n").map(row => row.split(","));

                let tbody = document.querySelector("#expendituresTable tbody");

                rows.slice(1).forEach(row => { // Skip the header row
                    let tr = document.createElement("tr");

                    row.forEach(cell => {
                        let td = document.createElement("td");
                        
                        // Clean up quotes and extra spaces
                        td.textContent = cell.replace(/['"]+/g, '').trim();

                        tr.appendChild(td);
                    });

                    tbody.appendChild(tr);
                });
            })
            .catch(error => console.error("CSV Load Error:", error));
        });
    </script>

</body>
</html>
