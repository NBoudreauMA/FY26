<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>FY26 Budget Expenditures</title>
    
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600&display=swap" rel="stylesheet">
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/chartjs-plugin-datalabels"></script>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Inter', sans-serif;
        }
        body {
            background-color: #f4f9f4;
            text-align: center;
            padding: 20px;
            overflow-x: hidden;
        }
        h1 {
            color: #2d6a4f;
            font-size: 2rem;
            margin-bottom: 20px;
        }
        .chart-container {
            width: 100%;
            max-width: 400px;
            height: 400px;
            margin: auto;
            background: rgba(255, 255, 255, 0.2);
            padding: 20px;
            border-radius: 15px;
            box-shadow: 0px 6px 12px rgba(0, 0, 0, 0.3);
            backdrop-filter: blur(10px);
            margin-bottom: 20px;
        }
        .dropdown-container {
            margin-bottom: 20px;
        }
        select {
            padding: 8px;
            font-size: 1rem;
        }
        .full-budget-container {
            width: 100%;
            max-width: 900px;
            margin: auto;
            background: white;
            border-radius: 8px;
            padding: 15px;
            box-shadow: 0px 4px 6px rgba(0, 0, 0, 0.1);
            margin-top: 30px;
            overflow-x: auto;
        }
        table {
            width: 100%;
            border-collapse: collapse;
        }
        th, td {
            border: 1px solid #ddd;
            padding: 10px;
            text-align: left;
            font-size: 0.9rem;
            white-space: nowrap;
        }
        th {
            background-color: #2d6a4f;
            color: white;
            position: sticky;
            top: 0;
            z-index: 2;
        }
        tr:nth-child(even) {
            background-color: #f1f8f1;
        }
    </style>
</head>
<body>
    <h1>FY26 Budget Expenditures</h1>
    
    <div class="chart-container">
        <h2>Where Your Tax Dollars Go</h2>
        <canvas id="taxDollarChart"></canvas>
    </div>
    
    <div class="dropdown-container">
        <label for="jumpTo">Jump to Department:</label>
        <select id="jumpTo" onchange="jumpToSection()">
            <option value="">Select...</option>
        </select>
    </div>
    
    <div class="full-budget-container">
        <h2>Full Budget Details</h2>
        <table id="budgetTable">
            <thead>
                <tr id="tableHeader">
                    <th>Department</th>
                    <th>Proposed Budget</th>
                </tr>
            </thead>
            <tbody>
                <tr><td>Loading budget data...</td></tr>
            </tbody>
        </table>
    </div>
    
    <script>
        document.addEventListener("DOMContentLoaded", function () {
            loadBudgetData();
            renderTaxChart();
        });

        function renderTaxChart() {
            const ctx = document.getElementById('taxDollarChart').getContext('2d');
            const budgetValues = [731340.38, 1581842.23, 920184.29, 7294874.64, 25550.00, 94289.70, 146862.00, 1004948.96];
            const totalBudget = budgetValues.reduce((acc, val) => acc + val, 0);
            const budgetPercentages = budgetValues.map(value => ((value / totalBudget) * 100).toFixed(2));
            
            new Chart(ctx, {
                type: 'doughnut',
                data: {
                    labels: ["General Government", "Public Safety", "Public Works", "Education", "Human Services", "Culture & Recreation", "Debt", "Liabilities & Assessments"],
                    datasets: [{
                        data: budgetPercentages,
                        backgroundColor: ['#43A047', '#388E3C', '#C0CA33', '#FFEB3B', '#FF9800', '#9C27B0', '#8E44AD', '#2ECC71'],
                        borderWidth: 2,
                        hoverOffset: 10
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: { position: 'bottom', labels: { color: 'black' } },
                        tooltip: {
                            callbacks: {
                                label: function(tooltipItem) {
                                    return tooltipItem.label + ": " + budgetPercentages[tooltipItem.dataIndex] + "%";
                                }
                            }
                        }
                    },
                    animation: {
                        animateScale: true,
                        animateRotate: true
                    }
                }
            });
        }

        async function loadBudgetData() {
            const csvUrl = "https://raw.githubusercontent.com/NBoudreauMA/FY26/main/docs/budget2.csv";
            try {
                const response = await fetch(csvUrl);
                if (!response.ok) throw new Error("Failed to load CSV file. Ensure the URL is correct.");
                const data = await response.text();
                populateBudgetTable(data);
            } catch (error) {
                document.querySelector("#budgetTable tbody").innerHTML = `<tr><td colspan="2">${error.message}</td></tr>`;
            }
        }

        function populateBudgetTable(csvText) {
            const tableBody = document.querySelector("#budgetTable tbody");
            const dropdown = document.getElementById("jumpTo");
            const rows = csvText.trim().split("\n").map(row => row.split(","));
            let tableContent = "";
            rows.slice(1).forEach(row => {
                tableContent += `<tr><td>${row[0].trim()}</td><td>${row[1].trim()}</td></tr>`;
                dropdown.innerHTML += `<option value="${row[0].trim()}">${row[0].trim()}</option>`;
            });
            tableBody.innerHTML = tableContent;
        }
    </script>
</body>
</html>
