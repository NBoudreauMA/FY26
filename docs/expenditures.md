<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Interactive Donut Chart</title>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600&display=swap" rel="stylesheet">
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
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
            max-width: 500px;
            margin: auto;
            margin-bottom: 20px;
        }
        .dropdown-container {
            margin-bottom: 20px;
        }
        select {
            padding: 8px;
            font-size: 1rem;
        }
        .table-container {
            width: 100%;
            max-width: 600px;
            margin: auto;
            background: white;
            border-radius: 8px;
            padding: 10px;
            box-shadow: 0px 4px 6px rgba(0, 0, 0, 0.1);
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
        }
        tr:nth-child(even) {
            background-color: #f1f8f1;
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
    </style>
</head>
<body>
    <h1>Interactive Donut Chart</h1>
    <p>This interactive chart provides a visual breakdown of the proposed budget allocations across various departments. Hover over each section to see detailed figures and use the dropdown to jump to specific budget sections.</p>
    <div class="chart-container">
        <canvas id="budgetChart"></canvas>
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
                <tr id="tableHeader"></tr>
            </thead>
            <tbody>
                <tr><td colspan="100%" class="error">Loading budget data...</td></tr>
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
                    labels: [
                        "General Government", "Public Safety", "Public Works", "Education", 
                        "Human Services", "Culture and Recreation", "Debt", "Liabilities and Assessments"
                    ],
                    datasets: [{
                        data: [
                            731340.38, 1581842.23, 920184.29, 7294874.64, 
                            25550.00, 94289.70, 146862.00, 1004948.96
                        ],
                        backgroundColor: ['#2d6a4f', '#52b788', '#74c69d', '#95d5b2', '#ff9800', '#9c27b0', '#8e44ad', '#2ecc71']
                    }]
                },
                options: { responsive: true, maintainAspectRatio: false, plugins: { legend: { position: 'bottom' }} }
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
                document.querySelector("#budgetTable tbody").innerHTML = `<tr><td colspan="100%">${error.message}</td></tr>`;
            }
        }
        function populateBudgetTable(csvText) {
            const tableHeader = document.querySelector("#tableHeader");
            const tableBody = document.querySelector("#budgetTable tbody");
            const dropdown = document.getElementById("jumpTo");
            const rows = csvText.trim().split("\n").map(row => row.split(","));
            tableHeader.innerHTML = rows[0].map(header => `<th>${header.trim()}</th>`).join("");
            let tableContent = "";
            let departmentSet = new Set();
            rows.slice(1).forEach(row => {
                let department = row[0].trim();
                let departmentId = department.replace(/\s+/g, '-').toLowerCase();
                if (!departmentSet.has(department)) {
                    departmentSet.add(department);
                    dropdown.innerHTML += `<option value="${departmentId}">${department}</option>`;
                }
                tableContent += `<tr id="${departmentId}">` + row.map(cell => `<td>${cell.trim()}</td>`).join("") + "</tr>";
            });
            tableBody.innerHTML = tableContent;
        }
        function jumpToSection() {
            const value = document.getElementById("jumpTo").value;
            if (value) document.getElementById(value).scrollIntoView({ behavior: 'smooth' });
        }
    </script>
</body>
</html>
