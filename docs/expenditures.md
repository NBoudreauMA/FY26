<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>FY26 Budget Expenditures</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 20px;
            background-color: #f8f9fa;
        }
        .container {
            max-width: 1200px;
            margin: 0 auto;
        }
        h1 {
            color: #5a2d82;
            text-align: center;
            margin-bottom: 1.5rem;
            font-size: 2rem;
        }
        .table-container {
            background: white;
            border-radius: 8px;
            box-shadow: 0 2px 4px rgba(0,0,0,0.1);
            overflow-x: auto;
        }
        table {
            width: 100%;
            border-collapse: collapse;
            margin: 0;
            table-layout: fixed;
        }
        th, td {
            padding: 12px;
            text-align: left;
            border: 1px solid #e2e8f0;
            word-wrap: break-word;
            overflow: hidden;
        }
        th {
            background-color: #5a2d82;
            color: white;
            font-weight: 600;
        }
        tr:nth-child(even) {
            background-color: #f8fafc;
        }
        td.number {
            text-align: right;
            font-family: 'Courier New', Courier, monospace;
        }
        .loading, .error {
            text-align: center;
            padding: 2rem;
            font-size: 1.1rem;
        }
        .error {
            color: #dc2626;
        }
        .total-row {
            background-color: #f3f0f5 !important;
            font-weight: 600;
        }
        thead {
            position: sticky;
            top: 0;
            background: #5a2d82;
            z-index: 2;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>FY26 Budget Expenditures</h1>
        <div class="table-container">
            <table id="budgetTable">
                <thead>
                    <tr>
                        <th>Department</th>
                        <th>Description</th>
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
                        <td colspan="9" class="loading">Loading budget data...</td>
                    </tr>
                </tbody>
            </table>
        </div>
    </div>

    <script>
        async function loadBudgetData() {
            try {
                const response = await fetch('https://raw.githubusercontent.com/NBoudreauMA/FY26/main/docs/budget.csv');
                if (!response.ok) {
                    throw new Error(`HTTP error! Status: ${response.status}`);
                }
                const data = await response.text();
                populateTable(data);
            } catch (error) {
                console.error('Error:', error);
                document.querySelector("#budgetTable tbody").innerHTML = 
                    `<tr><td colspan="9" class="error">Error loading budget data: ${error.message}</td></tr>`;
            }
        }

        function formatCurrency(value) {
            if (!value || isNaN(value)) return '-';
            return parseFloat(value).toLocaleString('en-US', { style: 'currency', currency: 'USD' });
        }

        function cleanNumber(value) {
            if (!value) return 0;
            return parseFloat(value.replace(/[$,"]/g, '')) || 0;
        }

        function populateTable(csvText) {
            const rows = csvText.split('\n').map(row => row.split(','));
            let tableBody = '';

            for (let i = 1; i < rows.length; i++) {
                const cols = rows[i];

                if (cols.length > 1) {
                    const isTotal = cols[4]?.trim().toUpperCase() === 'TOTAL';

                    tableBody += `<tr class="${isTotal ? 'total-row' : ''}">`;

                    // Department and Description
                    tableBody += `<td>${cols[1] || '-'}</td>`;
                    tableBody += `<td>${cols[4] || '-'}</td>`;

                    // Financial columns with formatting
                    for (let j = 5; j <= 11; j++) {
                        let value = cleanNumber(cols[j]);
                        tableBody += `<td class="number">${formatCurrency(value)}</td>`;
                    }

                    tableBody += '</tr>';
                }
            }

            document.querySelector("#budgetTable tbody").innerHTML = tableBody;
        }

        document.addEventListener('DOMContentLoaded', loadBudgetData);
    </script>
</body>
</html>
