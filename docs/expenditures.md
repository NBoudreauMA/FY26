<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Budget Expenditures</title>
    <link rel="stylesheet" href="assets/css/style.css">
</head>
<body>

    <h1>Budget Expenditures</h1>
    <p>This page provides an overview of the expenditures for the Town of Hubbardston.</p>

    <table id="expendituresTable" border="1">
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
            <!-- Data will be inserted here by JavaScript -->
        </tbody>
    </table>

    <script>
        document.addEventListener("DOMContentLoaded", function() {
            fetch('https://raw.githubusercontent.com/NBoudreauMA/FY26/main/docs/assets/budget.csv')
            .then(response => {
                if (!response.ok) {
                    throw new Error("HTTP error " + response.status);
                }
                return response.text();
            })
            .then(csv => {
                let rows = csv.trim().split("\n").map(row => row.split(","));
                let tbody = document.querySelector("#expendituresTable tbody");

                rows.slice(1).forEach(row => { // Skip the header row
                    let tr = document.createElement("tr");
                    row.forEach(cell => {
                        let td = document.createElement("td");
                        td.textContent = cell;
                        tr.appendChild(td);
                    });
                    tbody.appendChild(tr);
                });
            })
            .catch(error => console.error("CSV Load Error:", error));
        });
    </script>

</body>
</html>
