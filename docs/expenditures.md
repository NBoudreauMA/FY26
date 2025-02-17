<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>FY26 Budget Expenditures</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            background-color: #f5f5f5;
            margin: 0;
            padding: 20px;
        }

        h1, h2 {
            color: #5a2d82;
        }

        .container {
            width: 90%;
            margin: auto;
            background: white;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.1);
        }

        table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 20px;
            table-layout: auto; /* Ensures proper table scaling */
        }

        thead {
            position: sticky;
            top: 0;
            background-color: #5a2d82;
            color: white;
            z-index: 100;
        }

        th, td {
            border: 1px solid #ddd;
            padding: 8px;
            text-align: left;
            white-space: nowrap; /* Prevents header text from wrapping */
            overflow: hidden;
        }

        th {
            background-color: #5a2d82;
            color: white;
        }

        tbody tr:nth-child(even) {
            background-color: #f9f9f9;
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

    <div class="container">
        <table id="budgetTable">
            <thead>
                <tr id="headerRow">
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
                    <td colspan="9" class="error-message">Loading data...</td>
                </tr>
            </tbody>
        </table>
    </div>

    <script>
        document.addEventListener("DOMContentLoaded", function () {
            const csvUrl = "https://raw.githubusercontent.com/NBoudreauMA/FY26/main/docs/assets/budget.csv";

            fetch(csvUrl)
                .then(response => {
                    if (!response.ok) {
                        throw new Error("CSV file not found (404). Check the URL or file path.");
                    }
                    return response.text();
                })
                .then(data => {
                    const tableBody = document.querySelector("#budgetTable tbody");
                    tableBody.innerHTML = "";  // Clear the "Loading" message
                    
                    let rows = data.split("\n").map(row => row.split(","));
                    rows = rows.filter(row => row.some(cell => cell.trim() !== "")); // Remove empty rows

                    // Ensure headers are not repeated in the body
                    rows.shift(); // Remove the first row since it's the header
                    
                    rows.forEach(row => {
                        let tr = document.createElement("tr");

                        row.forEach(cell => {
                            let cleanedCell = cell.replace(/['"]+/g, '').trim(); // Remove quotes
                            let td = document.createElement("td");
                            td.textContent = cleanedCell;
                            tr.appendChild(td);
                        });

                        tableBody.appendChild(tr);
                    });
                })
                .catch(error => {
                    console.error("Error loading CSV:", error);
                    document.querySelector("#budgetTable tbody").innerHTML =
                        `<tr><td colspan="9" class="error-message">Error loading data</td></tr>`;
                });
        });
    </script>

</body>
</html>
