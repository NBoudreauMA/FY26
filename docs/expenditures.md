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
        }
        h1 {
            color: #5a2d82;
        }
        table {
            width: 80%;
            margin: 20px auto;
            border-collapse: collapse;
            text-align: left;
        }
        th, td {
            border: 1px solid #ddd;
            padding: 8px;
        }
        th {
            background-color: #5a2d82;
            color: white;
        }
        .error {
            color: red;
            font-weight: bold;
        }
    </style>
</head>
<body>

    <h1>FY26 Budget Expenditures</h1>
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
                <td colspan="9" class="error">Loading budget data...</td>
            </tr>
        </tbody>
    </table>

    <script>
        async function loadBudgetData() {
            const csvUrl = "https://raw.githubusercontent.com/NBoudreauMA/FY26/main/docs/budget.csv"; // Update with your raw GitHub CSV link
            try {
                const response = await fetch(csvUrl);
                if (!response.ok) throw new Error("Failed to load CSV file.");
                const data = await response.text();
                populateTable(data);
            } catch (error) {
                document.querySelector("#budgetTable tbody").innerHTML = `<tr><td colspan="9" class="error">Error loading budget data: ${error.message}</td></tr>`;
            }
        }

        function populateTable(csvText) {
            const rows = csvText.split("\n").map(row => row.split(","));
            let tableBody = "";
            rows.slice(1).forEach(row => {
                if (row.length > 1) {
                    tableBody += `<tr>${row.map(cell => `<td>${cell.trim()}</td>`).join("")}</tr>`;
                }
            });
            document.querySelector("#budgetTable tbody").innerHTML = tableBody;
        }

        loadBudgetData();
    </script>

</body>
</html>
