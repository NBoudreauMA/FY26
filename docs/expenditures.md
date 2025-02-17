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
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
            border-radius: 8px;
        }

        table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 20px;
            background-color: white;
        }

        thead {
            background-color: #5a2d82;
            color: white;
            font-weight: bold;
        }

        th, td {
            border: 1px solid #ddd;
            padding: 8px;
            text-align: left;
            white-space: nowrap;
        }

        tbody tr:nth-child(even) {
            background-color: #f9f9f9;
        }

        tbody tr:hover {
            background-color: #f1f1f1;
        }
    </style>
</head>
<body>
    <h1>FY26</h1>
    <h2>FY26 Budget Expenditures</h2>
    <p>This page provides an overview of the expenditures for the Town of Hubbardston.</p>

    <div class="container">
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
                <!-- Data will be dynamically inserted here -->
            </tbody>
        </table>
    </div>

    <script>
        document.addEventListener("DOMContentLoaded", function () {
            const tableBody = document.querySelector("#budgetTable tbody");
            const csvUrl = "https://raw.githubusercontent.com/YOURUSERNAME/YOURREPO/main/budget.csv"; // 🔹 Update this!

            fetch(csvUrl)
                .then(response => {
                    if (!response.ok) {
                        throw new Error("Failed to load CSV: " + response.statusText);
                    }
                    return response.text();
                })
                .then(csvText => {
                    const rows = csvText.split("\n").map(row => row.split(","));
                    rows.forEach((row, index) => {
                        if (row.length < 2 || row.every(cell => cell.trim() === "")) return; // Remove empty rows

                        const tr = document.createElement("tr");
                        row.forEach(cell => {
                            const td = document.createElement(index === 0 ? "th" : "td");
                            td.textContent = cell.trim();
                            tr.appendChild(td);
                        });
                        tableBody.appendChild(tr);
                    });
                })
                .catch(error => {
                    console.error("Error loading CSV:", error);
                    tableBody.innerHTML = `<tr><td colspan="9" style="color: red; text-align: center;">Error loading budget data</td></tr>`;
                });
        });
    </script>
</body>
</html>
