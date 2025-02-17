<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>FY26 Budget Expenditures</title>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script> <!-- Chart.js for visualization -->
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
        #chartContainer {
            width: 80%;
            margin: 20px auto;
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

    <div id="chartContainer">
        <canvas id="budgetChart"></canvas>
    </div>

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
            let departmentData = [];
            let expenseData = [];

            rows.slice(1).forEach(row => {
                if (row.length > 1) {
                    tableBody += "<tr>";
                    let department = "";
                    let fy26AdminValue = 0;

                    row.forEach((cell, index) => {
                        let cellValue = cell.trim();

                        // Fix Department & Category Spacing
                        if (index === 0 || index === 1) {
                            cellValue = cellValue
                                .replace(/([a-z])([A-Z])/g, '$1 $2') // Add space in camelCase text
                                .replace(/([0-9])([A-Za-z])/g, '$1 $2') // Add space between numbers and words
                                .replace(/([A-Za-z])([0-9])/g, '$1 $2') // Add space between words and numbers
                                .replace(/([A-Z])([A-Z][a-z])/g, '$1 $2') // Add space between uppercase acronyms & names
                                .replace(/[-_]/g, " "); // Ensure hyphenated and underscored words are properly spaced
                        }

                        // Fix Number Formatting: Remove spaces in large numbers (e.g., "1 500" → "1500")
                        cellValue = cellValue.replace(/"|\s(?=\d)/g, "");  // Remove extra spaces & quotes

                        // Convert numeric values correctly
                        if (!isNaN(cellValue) && cellValue !== "") {
                            cellValue = parseFloat(cellValue).toLocaleString(); // Format as number with commas
                        }

                        if (index === 0) department = cellValue; // Store department name
                        if (index === 6 && !isNaN(cellValue.replace(/,/g, ''))) {
                            fy26AdminValue = parseFloat(cellValue.replace(/,/g, '')); // Store FY26 Admin expenses
                        }

                        tableBody += `<td>${cellValue}</td>`;
                    });
                    tableBody += "</tr>";

                    // Add data to chart arrays
                    if (department && fy26AdminValue > 0) {
                        departmentData.push(department);
                        expenseData.push(fy26AdminValue);
                    }
                }
            });

            document.querySelector("#budgetTable tbody").innerHTML = tableBody;
            drawChart(departmentData, expenseData);
        }

        function drawChart(labels, data) {
            const ctx = document.getElementById("budgetChart").getContext("2d");

            new Chart(ctx, {
                type: "bar",
                data: {
                    labels: labels,
                    datasets: [{
                        label: "FY26 Admin Expenditures",
                        data: data,
                        backgroundColor: "rgba(90, 45, 130, 0.7)",
                        borderColor: "rgba(90, 45, 130, 1)",
                        borderWidth: 1
                    }]
                },
                options: {
                    responsive: true,
                    scales: {
                        y: {
                            beginAtZero: true
                        }
                    }
                }
            });
        }

        loadBudgetData();
    </script>

    <!-- Optional: Suppress the favicon.ico 404 error -->
    <link rel="icon" href="data:,">

</body>
</html>
