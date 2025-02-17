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
        h1, h2 {
            color: #5a2d82;
        }
        table {
            width: 90%;
            margin: auto;
            border-collapse: collapse;
            background-color: white;
            box-shadow: 0px 4px 8px rgba(0, 0, 0, 0.1);
        }
        thead {
            background-color: #5a2d82;
            color: white;
            position: sticky;
            top: 0;
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
        tbody tr:nth-child(even) {
            background-color: #f9f9f9;
        }
        tbody tr:hover {
            background-color: #f1f1f1;
        }
        .error {
            color: red;
            font-weight: bold;
        }
    </style>
</head>
<body>

    <h1>FY26</h1>
    <h2>FY26 Budget Expenditures</h2>
    <p>This page provides an overview of the expenditures for the Town of Hubbardston.</p>

    <div>
        <table id="budgetTable">
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
                <tr><td colspan="9" class="error">Loading budget data...</td></tr>
            </tbody>
        </table>
    </div>

    <script>
        document.addEventListener("DOMContentLoaded", function () {
            const csvUrl = 'docs/budget.csv'; // Ensure this matches actual location

            fetch(csvUrl)
                .then(response => {
                    if (!response.ok) {
                        throw new Error(`Failed to load CSV: ${response.statusText}`);
                    }
                    return response.text();
                })
                .then(data => parseCSV(data))
                .catch(error => {
                    console.error("CSV Load Error:", error);
                    document.querySelector("#budgetTable tbody").innerHTML = 
                        `<tr><td colspan="9" class="error">Error loading budget data: ${error.message}</td></tr>`;
                });

            function parseCSV(data) {
                const rows = data.split("\n").map(row => row.split(","));
                let tableBody = "";
                for (let i = 1; i < rows.length; i++) {  // Skip header row
                    if (rows[i].length < 9) continue; // Skip malformed rows
                    tableBody += `
                        <tr>
                            <td>${rows[i][0]}</td>
                            <td>${rows[i][1]}</td>
                            <td>${rows[i][2]}</td>
                            <td>${rows[i][3]}</td>
                            <td>${rows[i][4]}</td>
                            <td>${rows[i][5]}</td>
                            <td>${rows[i][6]}</td>
                            <td>${rows[i][7]}</td>
                            <td>${rows[i][8]}</td>
                        </tr>
                    `;
                }
                document.querySelector("#budgetTable tbody").innerHTML = tableBody || 
                    `<tr><td colspan="9" class="error">No budget data found.</td></tr>`;
            }
        });
    </script>

</body>
</html>
