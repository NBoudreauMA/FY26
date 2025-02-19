<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Expenditures</title>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <link rel="stylesheet" href="assets/css/style.css">
</head>
<body>
    <h1>Expenditures Breakdown</h1>
    <div class="chart-container">
        <canvas id="budgetChart"></canvas>
    </div>

    <div class="full-budget-container">
        <h2>Full Budget Details</h2>
        <table id="budgetTable">
            <thead>
                <tr id="tableHeader"></tr>
            </thead>
            <tbody>
                <tr><td colspan="100%">Loading budget data...</td></tr>
            </tbody>
        </table>
    </div>

    <script>
        document.addEventListener("DOMContentLoaded", function () {
            renderChart();
            loadBudgetData();
        });

        function renderChart() {
            const ctx = document.getElementById('budgetChart').getContext('2d');
            new Chart(ctx, {
                type: 'doughnut',
                data: {
                    labels: ["General Government", "Public Safety", "Public Works", "Education"],
                    datasets: [{
                        data: [731340, 1581842, 920184, 7294874],
                        backgroundColor: ['#2d6a4f', '#52b788', '#74c69d', '#95d5b2']
                    }]
                },
                options: { responsive: true, maintainAspectRatio: false }
            });
        }

        async function loadBudgetData() {
            const csvUrl = "/FY26/assets/budget2.csv";
            try {
                const response = await fetch(csvUrl);
                if (!response.ok) throw new Error("Failed to load CSV.");
                const data = await response.text();
                populateBudgetTable(data);
            } catch (error) {
                document.querySelector("#budgetTable tbody").innerHTML = `<tr><td colspan="100%">${error.message}</td></tr>`;
            }
        }

        function populateBudgetTable(csvText) {
            const tableHeader = document.querySelector("#tableHeader");
            const tableBody = document.querySelector("#budgetTable tbody");
            const rows = csvText.trim().split("\n").map(row => row.split(","));
            tableHeader.innerHTML = rows[0].map(header => `<th>${header}</th>`).join("");
            tableBody.innerHTML = rows.slice(1).map(row => `<tr>${row.map(cell => `<td>${cell}</td>`).join("")}</tr>`).join("");
        }
    </script>
</body>
</html>
