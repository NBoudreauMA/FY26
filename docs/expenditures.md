<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>FY26 Budget Expenditures</title>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            padding: 20px;
        }
        h1 {
            color: #2d6a4f;
        }
        .table-container {
            width: 100%;
            overflow-x: auto;
            max-height: 600px;
            overflow-y: auto;
        }
        table {
            width: 100%;
            border-collapse: collapse;
            table-layout: auto;
            min-width: 100%;
            white-space: nowrap;
        }
        th, td {
            border: 1px solid #ddd;
            padding: 8px;
            text-align: left;
        }
        th {
            background-color: #2d6a4f;
            color: white;
            position: sticky;
            top: 0;
            z-index: 2;
        }
        .scrollable {
            display: block;
            overflow-x: auto;
            max-width: 100%;
        }
    </style>
</head>
<body>

    <h1>FY26 Budget Expenditures</h1>
    
    <div class="table-container">
        <table id="budgetTable" class="scrollable">
            <thead>
                <tr id="tableHeader"></tr>
            </thead>
            <tbody>
                <tr>
                    <td colspan="100%" class="error">Loading budget data...</td>
                </tr>
            </tbody>
        </table>
    </div>

    <script>
        document.addEventListener("DOMContentLoaded", function () {
            loadBudgetData();
        });

        async function loadBudgetData() {
            const csvUrl = "https://raw.githubusercontent.com/NBoudreauMA/FY26/main/docs/budget2.csv";
            try {
                const response = await fetch(csvUrl);
                if (!response.ok) throw new Error("Failed to load CSV file. Ensure the URL is correct.");
                const data = await response.text();
                populateTable(data);
            } catch (error) {
                document.querySelector("#budgetTable tbody").innerHTML = `<tr><td colspan="100%">${error.message}</td></tr>`;
            }
        }

        function populateTable(csvText) {
            const tableHeader = document.querySelector("#tableHeader");
            const tableBody = document.querySelector("#budgetTable tbody");
            const rows = csvText.trim().split("\n").map(row => row.split(","));
            
            tableHeader.innerHTML = rows[0].map(header => `<th>${header.trim()}</th>`).join("");
            let tableContent = "";
            rows.slice(1).forEach(row => {
                tableContent += "<tr>";
                row.forEach((cell, index) => {
                    let cellValue = cell.trim();
                    if (index === rows[0].length - 1) {
                        // Keep the last column as percentage if applicable
                        tableContent += cellValue && !isNaN(parseFloat(cellValue)) ? `<td>${parseFloat(cellValue).toFixed(2)}%</td>` : "<td></td>";
                    } else {
                        // Format all other numerical values as currency
                        const numValue = parseFloat(cellValue);
                        tableContent += isNaN(numValue) ? `<td>${cellValue}</td>` : `<td>$${numValue.toLocaleString()}</td>`;
                    }
                });
                tableContent += "</tr>";
            });
            tableBody.innerHTML = tableContent;
        }
    </script>

</body>
</html>
