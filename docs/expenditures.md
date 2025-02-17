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
            width: 90%;
            margin: 20px auto;
            border-collapse: collapse;
            text-align: left;
        }
        th, td {
            border: 1px solid #ddd;
            padding: 8px;
            text-align: right;
        }
        th {
            background-color: #5a2d82;
            color: white;
            text-align: center;
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
            const csvUrl = "https://raw.githubusercontent.com/NBoudreauMA/FY26/main/docs/budget.csv"; // Update with correct CSV link

            try {
                const response = await fetch(csvUrl);
                if (!response.ok) throw new Error("Failed to load CSV file. Ensure the URL is correct.");

                const data = await response.text();
                populateTable(data);
            } catch (error) {
                document.querySelector("#budgetTable tbody").innerHTML = `<tr><td colspan="9" class="error">${error.message}</td></tr>`;
            }
        }

        function populateTable(csvText) {
            const rows = csvText.trim().split("\n").map(row => row.split(","));
            let tableBody = "";

            rows.slice(1).forEach(row => {
                if (row.length > 1) {
                    tableBody += "<tr>";
                    row.forEach((cell) => {
                        let cellValue = cell.trim();

                        // Fix Number Formatting: Remove spaces in large numbers (e.g., "1 500" → "1500")
                        cellValue = cellValue.replace(/"|\s/g, "");  // Remove extra spaces & quotes

                        // Convert numeric values correctly
                        if (!isNaN(cellValue) && cellValue !== "") {
                            cellValue = parseFloat(cellValue).toLocaleString(); // Format as number with commas
                        }

                        tableBody += `<td>${cellValue}</td>`;
                    });
                    tableBody += "</tr>";
                }
            });

            document.querySelector("#budgetTable tbody").innerHTML = tableBody;
        }

        loadBudgetData();
    </script>

</body>
</html>
