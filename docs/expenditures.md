<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>FY26 Budget Expenditures</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 20px;
        }
        h1 {
            color: #4a0080;
        }
        table {
            width: 100%;
            border-collapse: collapse;
            table-layout: fixed;
        }
        th, td {
            border: 1px solid #000;
            padding: 8px;
            text-align: left;
            white-space: nowrap;
        }
        th {
            background-color: #f2f2f2;
            position: sticky;
            top: 0;
            z-index: 2;
        }
        .table-container {
            max-height: 600px;
            overflow-y: auto;
            border: 1px solid #ddd;
        }
    </style>
</head>
<body>

    <h1>FY26 Budget Expenditures</h1>
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
            <tbody></tbody>
        </table>
    </div>

    <script>
        async function loadCSV() {
            const response = await fetch('https://raw.githubusercontent.com/NBoudreauMA/FY26/main/assets/budget.csv');
            const data = await response.text();
            const rows = data.split("\n").map(row => row.split(","));

            let tableBody = document.querySelector("#budgetTable tbody");
            tableBody.innerHTML = "";

            rows.forEach((row, index) => {
                if (row.length > 1) {
                    let tr = document.createElement("tr");
                    row.forEach(cell => {
                        let td = document.createElement("td");
                        td.textContent = cell.replace(/"/g, '');
                        tr.appendChild(td);
                    });
                    tableBody.appendChild(tr);
                }
            });
        }

        loadCSV();
    </script>

</body>
</html>
