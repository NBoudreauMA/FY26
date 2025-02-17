<html lang="en"><!DOCTYPE html>
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
            table-layout: fixed;
        }
        th, td {
            border: 1px solid black;
            padding: 8px;
            text-align: left;
            white-space: nowrap;
        }
        th {
            background-color: #f2f2f2;
        }
        td[colspan] {
            font-weight: bold;
            background-color: #e0e0e0;
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
                let rows = csv.trim().split("\n");
                let tbody = document.querySelector("#expendituresTable tbody");

                rows.slice(1).forEach(row => { // Skip header row
                    let columns = row.match(/(".*?"|[^",]+)(?=\s*,|\s*$)/g);

                    let tr = document.createElement("tr");

                    columns.forEach((cell, index) => {
                        let td = document.createElement("td");

                        // If it's a department header, merge cells
                        if (index === 0 && columns.length < 9) {
                            td.setAttribute("colspan", "9");
                            td.style.textAlign = "left";
                            td.style.fontWeight = "bold";
                            td.style.backgroundColor = "#e0e0e0";
                        } else {
                            td.textContent = cell.replace(/^"|"$/g, '').trim();
                        }

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
            padding: 6px;
            text-align: left;
            white-space: nowrap;
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
                let rows = csv.trim().split("\n");

                let tbody = document.querySelector("#expendituresTable tbody");

                rows.slice(1).forEach(row => { // Skip the header row
                    // Handle quoted CSV values properly
                    let columns = row.match(/(".*?"|[^",]+)(?=\s*,|\s*$)/g);

                    let tr = document.createElement("tr");

                    columns.forEach(cell => {
                        let td = document.createElement("td");

                        // Remove surrounding quotes and trim whitespace
                        td.textContent = cell.replace(/^"|"$/g, '').trim();
                        
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
