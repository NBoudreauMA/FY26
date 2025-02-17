<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>FY26 Budget Expenditures</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 20px;
            padding: 0;
            background-color: #f8f9fa;
        }
        h1 {
            color: #5A2E8C;
        }
        h2 {
            color: #5A2E8C;
        }
        table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 20px;
            background-color: white;
        }
        th, td {
            border: 1px solid black;
            padding: 8px;
            text-align: left;
        }
        th {
            background-color: #5A2E8C;
            color: white;
            position: sticky;
            top: 0;
            z-index: 100;
        }
        tbody {
            overflow-y: auto;
            height: 500px;
            display: block;
        }
        tr {
            display: table;
            width: 100%;
            table-layout: fixed;
        }
        th:first-child, td:first-child {
            font-weight: bold;
        }
    </style>
</head>
<body>
    <h1><a href="index.html" style="text-decoration: none; color: #5A2E8C;">FY26</a></h1>
    <h2>FY26 Budget Expenditures</h2>
    <p>This page provides an overview of the expenditures for the Town of Hubbardston.</p>

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

    <script>
        async function loadCSV() {
            try {
                const response = await fetch('https://raw.githubusercontent.com/NBoudreauMA/FY26/main/assets/budget.csv');
                if (!response.ok) {
                    throw new Error("CSV file could not be loaded.");
                }
                const data = await response.text();

                // Normalize line breaks for compatibility
                const rows = data.trim().split(/\r?\n/).map(row => row.split(","));

                let tableBody = document.querySelector("#budgetTable tbody");
                tableBody.innerHTML = "";

                rows.forEach((row, index) => {
                    if (row.length > 1) {
                        let tr = document.createElement("tr");
                        row.forEach(cell => {
                            let td = document.createElement(index === 0 ? "th" : "td");
                            td.textContent = cell.replace(/"/g, '').trim();
                            tr.appendChild(td);
                        });
                        tableBody.appendChild(tr);
                    }
                });
            } catch (error) {
                console.error("Error loading CSV:", error);
            }
        }

        loadCSV();
    </script>
</body>
</html>
