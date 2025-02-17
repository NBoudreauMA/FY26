<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>FY26 Budget Expenditures</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f8f9fa;
            text-align: center;
            margin: 0;
        }
        h1, h2 {
            color: #5a2d82;
            margin-bottom: 5px;
        }
        .table-container {
            width: 95%;
            max-height: 80vh;
            overflow-y: auto;
            margin: 20px auto;
            border: 1px solid #ddd;
            background: white;
        }
        table {
            width: 100%;
            border-collapse: collapse;
            background-color: white;
            table-layout: fixed;
        }
        th, td {
            border: 1px solid #ddd;
            padding: 10px;
            text-align: center;
            vertical-align: middle;
            white-space: nowrap;
            overflow: hidden;
            text-overflow: ellipsis;
        }
        th {
            background-color: #5a2d82;
            color: white;
            font-weight: bold;
            position: sticky;
            top: 0;
            z-index: 2;
        }
        tr:nth-child(even) {
            background-color: #f2f2f2;
        }
        .error-message {
            color: red;
            font-weight: bold;
        }
    </style>
</head>
<body>
    <h1><a href="index.html" style="text-decoration: none; color: #5a2d82;">FY26</a></h1>
    <h2>FY26 Budget Expenditures</h2>
    <p>This page provides an overview of the expenditures for the Town of Hubbardston.</p>

    <div class="table-container">
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
            <tbody id="tableBody">
                <tr>
                    <td colspan="9" class="error-message">Loading data...</td>
                </tr>
            </tbody>
        </table>
    </div>

    <script>
        async function loadCSV() {
            const csvUrl = 'https://raw.githubusercontent.com/NBoudreauMA/FY26/main/docs/assets/budget.csv';
            try {
                const response = await fetch(csvUrl);
                if (!response.ok) throw new Error('CSV file not found');

                const csvText = await response.text();
                const rows = csvText.split('\n').map(row => row.split(',').map(cell => cell.replace(/['"]+/g, '').trim()));

                let tableBody = document.querySelector("#tableBody");
                tableBody.innerHTML = ""; // Clear error message

                rows.slice(1).forEach(row => {  // Skip the header
                    if (row.length > 1 && row.some(cell => cell.trim() !== "")) { // Ignore empty lines
                        let tr = document.createElement("tr");

                        row.forEach(cell => {
                            let td = document.createElement("td");
                            td.textContent = cell.replace(/\s?000$/, ''); // Fix number format issue
                            tr.appendChild(td);
                        });

                        tableBody.appendChild(tr);
                    }
                });

            } catch (error) {
                document.querySelector(".error-message").textContent = "Error loading data";
            }
        }
        window.onload = loadCSV;
    </script>
</body>
</html>
