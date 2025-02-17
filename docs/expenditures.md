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

        tbody tr:nth-child(even) {
            background-color: #f9f9f9;
        }

        tbody tr:hover {
            background-color: #f1f1f1;
        }

        .container {
            overflow-y: auto;
            max-height: 80vh; /* Allows vertical scrolling */
            margin-top: 10px;
        }
    </style>
</head>
<body>

    <h1>FY26</h1>
    <h2>FY26 Budget Expenditures</h2>
    <p>This page provides an overview of the expenditures for the Town of Hubbardston.</p>

    <div class="container">
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
                <!-- Data will be dynamically inserted here -->
            </tbody>
        </table>
    </div>

    <script>
        async function loadCSV() {
            try {
                const response = await fetch("budget.csv");
                const data = await response.text();
                const rows = data.split("\n").map(row => row.split(","));

                let tableBody = document.querySelector("#budgetTable tbody");
                tableBody.innerHTML = ""; 

                for (let i = 1; i < rows.length; i++) { 
                    let row = document.createElement("tr");

                    rows[i].forEach(cell => {
                        let cellElement = document.createElement("td");
                        cellElement.textContent = cell.trim();
                        row.appendChild(cellElement);
                    });

                    tableBody.appendChild(row);
                }
            } catch (error) {
                console.error("Error loading data:", error);
                let tableBody = document.querySelector("#budgetTable tbody");
                tableBody.innerHTML = `<tr><td colspan="9" style="text-align:center; color: red;">Error loading data</td></tr>`;
            }
        }

        document.addEventListener("DOMContentLoaded", loadCSV);
    </script>

</body>
</html>
