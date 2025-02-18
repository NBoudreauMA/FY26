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
            overflow: hidden;
            max-height: 80vh;
            overflow-y: auto;
        }
        table {
            width: 100%;
            border-collapse: collapse;
            margin: 0;
            position: relative;
        }
        th, td {
            padding: 12px;
            text-align: left;
            border: 1px solid #e2e8f0;
        }
        th {
            background-color: #5a2d82;
            color: white;
            font-weight: 600;
            position: sticky;
            top: 0;
            z-index: 2;
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
                const response = await fetch(
                    'https://raw.githubusercontent.com/NBoudreauMA/FY26/main/docs/budget.csv'
                );
                if (!response.ok) {
                    throw new Error(`HTTP error! status: ${response.status}`);
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
            if (!value || value === '') return '-';
            const num = parseFloat(value.replace(/[$,]/g, '') || 0);
            return num.toLocaleString('en-US', { style: 'currency', currency: 'USD' });
        }

        function populateTable(csvText) {
            const rows = csvText.split('\n').map(row => row.split(','));
            let tableBody = '';

            // Skip header row, start from index 1
            for (let i = 1; i < rows.length; i++) {
                const cols = rows[i].map(col => col.trim());
                if (cols.length > 1) {
                    const isTotal = cols[4] === 'TOTAL';
                    tableBody += `<tr class="${isTotal ? 'total-row' : ''}">`;
                    
                    // Department and Description
                    tableBody += `<td>${cols[0] || '-'}</td>`;
                    tableBody += `<td>${cols[1] || '-'}</td>`;

                    // Financial columns
                    for (let j = 2; j <= 8; j++) {
                        const value = cols[j] || '-';
                        tableBody += `<td class="number">${j < 8 ? formatCurrency(value) : value}</td>`;
                    }
                    
                    tableBody += '</tr>';
                }
            }
            
            document.querySelector("#budgetTable tbody").innerHTML = tableBody;
        }

        // Load data when page loads
        document.addEventListener('DOMContentLoaded', loadBudgetData);
    </script>
</body>
</html>
