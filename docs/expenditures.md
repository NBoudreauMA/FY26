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
            color: #5a2d82;
        }
        .table-container {
            width: 100%;
            overflow-x: auto;
        }
        table {
            width: 100%;
            border-collapse: collapse;
            table-layout: fixed;
            min-width: 1500px;
        }
        th, td {
            border: 1px solid #ddd;
            padding: 8px;
            text-align: right;
            overflow: hidden;
            text-overflow: ellipsis;
            white-space: nowrap;
        }
        th {
            background-color: #5a2d82;
            color: white;
            text-align: center;
        }
        #chartContainer {
            width: 80%;
            margin: 30px auto;
        }
    </style>
</head>
<body>

    <h1>FY26 Budget Expenditures</h1>
    
    <div class="table-container">
        <table id="budgetTable">
            <thead>
                <tr id="tableHeader"></tr>
            </thead>
            <tbody>
                <tr>
                    <td colspan="9" class="error">Loading budget data...</td>
                </tr>
            </tbody>
        </table>
    </div>

    <div id="chartContainer">
        <canvas id="budgetChart"></canvas>
    </div>

    <script>
        document.addEventListener("DOMContentLoaded", function () {
            loadBudgetData();
        });

        async function loadBudgetData() {
            const csvUrl = "https://raw.githubusercontent.com/NBoudreauMA/FY26/main/docs/budget.csv";

            try {
                const response = await fetch(csvUrl);
                if (!response.ok) throw new Error("Failed to load CSV file. Ensure the URL is correct.");
                const data = await response.text();
                populateTable(data);
            } catch (error) {
                const tableBody = document.querySelector("#budgetTable tbody");
                if (tableBody) {
                    tableBody.innerHTML = `<tr><td colspan="9" class="error">${error.message}</td></tr>`;
                }
            }
        }

        function populateTable(csvText) {
            const tableHeader = document.querySelector("#tableHeader");
            const tableBody = document.querySelector("#budgetTable tbody");
            
            const rows = csvText.trim().split("\n").map(row => row.split(","));
            tableHeader.innerHTML = rows[0].map(header => `<th>${header.trim()}</th>`).join("");
            
            let tableContent = "";
            let departmentData = [];
            let expenseData = [];

            rows.slice(1).forEach(row => {
                if (row.length > 1) {
                    tableContent += "<tr>";
                    let department = "";
                    let fy26AdminValue = 0;

                    row.forEach((cell, index) => {
                        let cellValue = cell.trim();
                        if (!isNaN(cellValue) && cellValue !== "") {
                            cellValue = parseFloat(cellValue.replace(/,/g, '')).toLocaleString();
                        }
                        if (index === 0) department = cellValue;
                        if (index === 6 && !isNaN(cellValue.replace(/,/g, ''))) {
                            fy26AdminValue = parseFloat(cellValue.replace(/,/g, ''));
                        }
                        tableContent += `<td>${cellValue}</td>`;
                    });
                    tableContent += "</tr>";

                    if (department && fy26AdminValue > 0) {
                        departmentData.push(department);
                        expenseData.push(fy26AdminValue);
                    }
                }
            });

            tableBody.innerHTML = tableContent;
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
                    maintainAspectRatio: false,
                    scales: {
                        y: {
                            beginAtZero: true
                        }
                    }
                }
            });
        }
    </script>

</body>
</html>
