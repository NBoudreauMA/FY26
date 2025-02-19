<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>FY26 Budget Expenditures</title>
    
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
    <h1>FY26 Budget Expenditures</h1>
    
    <div class="chart-container">
        <canvas id="budgetChart"></canvas>
    </div>
    
    <div class="dropdown-container">
        <label for="jumpTo">Jump to Department:</label>
        <select id="jumpTo" onchange="jumpToSection()">
            <option value="">Select...</option>
            <option value="general">General Government</option>
            <option value="safety">Public Safety</option>
            <option value="works">Public Works</option>
            <option value="education">Education</option>
            <option value="human">Human Services</option>
            <option value="culture">Culture and Recreation</option>
            <option value="debt">Debt</option>
            <option value="liabilities">Liabilities and Assessments</option>
        </select>
    </div>
    
    <div class="table-container">
        <table>
            <thead>
                <tr>
                    <th>Department</th>
                    <th>Proposed Budget</th>
                </tr>
            </thead>
            <tbody id="summaryTableBody">
                <tr id="general"><td>General Government</td><td>$731,340.38</td></tr>
                <tr id="safety"><td>Public Safety</td><td>$1,581,842.23</td></tr>
                <tr id="works"><td>Public Works</td><td>$920,184.29</td></tr>
                <tr id="education"><td>Education</td><td>$7,294,874.64</td></tr>
                <tr id="human"><td>Human Services</td><td>$25,550.00</td></tr>
                <tr id="culture"><td>Culture and Recreation</td><td>$94,289.70</td></tr>
                <tr id="debt"><td>Debt</td><td>$146,862.00</td></tr>
                <tr id="liabilities"><td>Liabilities and Assessments</td><td>$1,004,948.96</td></tr>
            </tbody>
        </table>
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
            loadBudgetData();
            renderChart();
        });

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
            const rows = csvText.trim().split("\n").map(row => row.split(","));
            
            tableHeader.innerHTML = rows[0].map(header => `<th>${header.trim()}</th>`).join("");
            let tableContent = "";
            
            rows.slice(1).forEach(row => {
                tableContent += "<tr>" + row.map(cell => `<td>${cell.trim()}</td>`).join("") + "</tr>";
            });
            tableBody.innerHTML = tableContent;
        }

        function renderChart() {
            const ctx = document.getElementById('budgetChart').getContext('2d');
            new Chart(ctx, {
                type: 'pie',
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
                        backgroundColor: ['#FF6384', '#36A2EB', '#FFCE56', '#4CAF50', '#FF9800', '#9C27B0', '#8E44AD', '#2ECC71']
                    }]
                },
                options: { responsive: true, maintainAspectRatio: false, plugins: { legend: { position: 'bottom' }}}
            });
        }

        function jumpToSection() {
            const value = document.getElementById("jumpTo").value;
            if (value) document.getElementById(value).scrollIntoView({ behavior: 'smooth' });
        }
    </script>
</body>
</html>
