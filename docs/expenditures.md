<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>FY26 Budget Expenditures</title>
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/PapaParse/5.3.0/papaparse.min.js"></script>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            background-color: #f4f4f4;
        }
        h1 {
            color: #4A148C;
        }
        table {
            border-collapse: collapse;
            width: 90%;
            margin: 20px auto;
            background: white;
        }
        th, td {
            border: 1px solid #ddd;
            padding: 8px;
            text-align: left;
            white-space: nowrap;
        }
        th {
            background-color: #4A148C;
            color: white;
            position: sticky;
            top: 0;
            z-index: 2;
        }
        .table-container {
            width: 90%;
            max-height: 80vh;
            overflow-y: auto;
            margin: auto;
            border: 1px solid #ddd;
            background: white;
        }
        .error {
            color: red;
            font-weight: bold;
        }
    </style>
</head>
<body>
    <h1><a href="index.html" style="text-decoration: none; color: #4A148C;">FY26</a></h1>
    <h2 style="color: #4A148C;">FY26 Budget Expenditures</h2>
    <p>This page provides an overview of the expenditures for the Town of Hubbardston.</p>

    <div class="table-container">
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
                <tr id="loadingMessage">
                    <td colspan="9">Loading data...</td>
                </tr>
            </tbody>
        </table>
    </div>

    <script>
        $(document).ready(function() {
            const csvUrl = "https://raw.githubusercontent.com/NBoudreauMA/FY26/main/docs/assets/budget.csv";

            console.log("Fetching CSV data from:", csvUrl);

            Papa.parse(csvUrl, {
                download: true,
                header: true,
                skipEmptyLines: true,
                complete: function(results) {
                    console.log("CSV Data Parsed:", results.data);
                    const data = results.data;
                    const tableBody = $("#budgetTable tbody");
                    tableBody.empty();

                    if (data.length === 0) {
                        tableBody.append("<tr><td colspan='9' class='error'>No data available</td></tr>");
                        return;
                    }

                    data.forEach(row => {
                        if (!row["Department"]) return; // Skip empty rows
                        const newRow = `
                            <tr>
                                <td>${row["Department"] || ""}</td>
                                <td>${row["Category"] || ""}</td>
                                <td>${row["FY24"] || ""}</td>
                                <td>${row["FY25 Request"] || ""}</td>
                                <td>${row["FY25"] || ""}</td>
                                <td>${row["FY26 Dept"] || ""}</td>
                                <td>${row["FY26 Admin"] || ""}</td>
                                <td>${row["Change ($)"] || ""}</td>
                                <td>${row["Change (%)"] || ""}</td>
                            </tr>`;
                        tableBody.append(newRow);
                    });
                },
                error: function() {
                    console.log("Error: Failed to load CSV.");
                    $("#budgetTable tbody").html("<tr><td colspan='9' class='error'>Error loading data</td></tr>");
                }
            });
        });
    </script>
</body>
</html>
