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
        }
        h1, h2 {
            color: #5a2d82;
        }
        table {
            width: 90%;
            margin: 20px auto;
            border-collapse: collapse;
            background-color: white;
            box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.1);
        }
        th, td {
            border: 1px solid #ddd;
            padding: 10px;
            text-align: left;
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
        #error {
            color: red;
            font-weight: bold;
        }
    </style>
</head>
<body>
    <h1><a href="index.html" style="text-decoration: none; color: #5a2d82;">FY26</a></h1>
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
            <tr id="errorRow">
                <td colspan="9" id="error">Loading data...</td>
            </tr>
        </tbody>
    </table>

    <script>
        async function loadCSV() {
            const csvUrl = 'https://raw.githubusercontent.com/NBoudreauMA/FY26/main/docs/assets/budget.csv';
            try {
                const response = await fetch(csvUrl);
                if (!response.ok) throw new Error('CSV file not found');

                const csvText = await response.text();
                const rows = csvText.split('\n').map(row => row.split(','));

                let tableBody = document.querySelector("#budgetTable tbody");
                tableBody.innerHTML = ""; // Clear error message

                rows.slice(1).forEach(row => {  // Skip the header
                    if (row.length > 1) { // Ignore empty lines
                        let tr = document.createElement("tr");
                        row.forEach(cell => {
                            let td = document.createElement("td");
                            td.textContent = cell.trim();
                            tr.appendChild(td);
                        });
                        tableBody.appendChild(tr);
                    }
                });

            } catch (error) {
                document.getElementById("error").textContent = "Error loading data";
            }
        }
        window.onload = loadCSV;
    </script>
</body>
</html>
