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
            padding: 20px;
            background-color: #f8f9fa;
        }
        h1 {
            color: #6a0dad;
        }
        h2 {
            color: #6a0dad;
        }
        table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 20px;
            background-color: #ffffff;
        }
        th, td {
            border: 1px solid #ddd;
            padding: 8px;
            text-align: left;
        }
        th {
            background-color: #6a0dad;
            color: white;
            position: sticky;
            top: 0;
            z-index: 2;
        }
        tr:nth-child(even) {
            background-color: #f2f2f2;
        }
        tr:hover {
            background-color: #ddd;
        }
    </style>
</head>
<body>

    <h1><a href="index.html" style="text-decoration: none; color: #6a0dad;">FY26</a></h1>
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
        <tbody>
            <tr>
                <td colspan="9" style="text-align:center;">Loading data...</td>
            </tr>
        </tbody>
    </table>

    <script>
        async function loadCSV() {
            try {
                const csvUrl = 'https://raw.githubusercontent.com/NBoudreauMA/FY26/main/assets/budget.csv';
                const response = await fetch(csvUrl);
                if (!response.ok) {
                    throw new Error(`CSV file could not be loaded. HTTP Status: ${response.status}`);
                }
                const data = await response.text();

                console.log("CSV Loaded Successfully!");
                console.log("Raw CSV Data:", data); // Debugging step

                // Normalize line breaks & parse CSV
                let rows = data.trim().split(/\r?\n/).map(row => row.split(/,(?=(?:(?:[^"]*"){2})*[^"]*$)/));

                // Check if rows were parsed correctly
                console.log("Parsed CSV Data:", rows);

                if (rows.length === 0 || rows[0].length < 2) {
                    throw new Error("CSV parsing failed - no valid data found.");
                }

                let tableBody = document.querySelector("#budgetTable tbody");
                tableBody.innerHTML = "";

                rows.forEach((row, index) => {
                    let tr = document.createElement("tr");
                    row.forEach(cell => {
                        let td = document.createElement(index === 0 ? "th" : "td");
                        td.textContent = cell.replace(/"/g, '').trim(); // Remove extra quotes
                        tr.appendChild(td);
                    });
                    tableBody.appendChild(tr);
                });

            } catch (error) {
                console.error("Error loading CSV:", error);
                document.querySelector("#budgetTable tbody").innerHTML = `<tr><td colspan="9" style="color: red; text-align: center;">Error loading data</td></tr>`;
            }
        }

        loadCSV();
    </script>

</body>
</html>
