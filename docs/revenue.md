<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>FY26 Hubbardston Revenue Breakdown</title>
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
            background: linear-gradient(135deg, #2c6e49, #1e3d32);
            color: white;
            text-align: center;
            padding: 20px;
        }
        h1 {
            font-size: 3.5rem;
            margin-bottom: 30px;
            text-shadow: 4px 4px 6px rgba(0, 0, 0, 0.5);
        }
        .chart-container {
            width: 100%;
            max-width: 600px;
            margin: auto;
            padding: 25px;
            background: rgba(255, 255, 255, 0.2);
            border-radius: 20px;
            box-shadow: 0px 10px 20px rgba(0, 0, 0, 0.4);
        }
        .folder {
            width: 80%;
            max-width: 700px;
            margin: 20px auto;
            background: rgba(255, 255, 255, 0.2);
            padding: 10px;
            border-radius: 10px;
            box-shadow: 0px 5px 10px rgba(0, 0, 0, 0.3);
            cursor: pointer;
        }
        .folder h2 {
            margin: 0;
            padding: 10px;
            background: #388E3C;
            border-radius: 8px;
            text-align: left;
            padding-left: 15px;
        }
        .folder-content {
            display: none;
            padding: 15px;
            text-align: left;
            background: rgba(255, 255, 255, 0.1);
            border-radius: 8px;
        }
        table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 10px;
            background: rgba(255, 255, 255, 0.1);
            border-radius: 8px;
            overflow: hidden;
        }
        th, td {
            border: 1px solid white;
            padding: 8px;
            text-align: left;
            font-size: 1rem;
        }
        th {
            background: #388E3C;
        }
    </style>
</head>
<body>
    <h1>FY26 Hubbardston Revenue Breakdown</h1>
    
    <div class="chart-container">
        <canvas id="revenueChart"></canvas>
    </div>
    
    <p>The following sections break down Hubbardston’s revenue sources for FY26. Click each section to expand and view more details.</p>
    
    <script>
        document.addEventListener("DOMContentLoaded", function () {
            const ctx = document.getElementById("revenueChart").getContext("2d");
            new Chart(ctx, {
                type: "doughnut",
                data: {
                    labels: ["Tax Levy", "State Aid", "Local Receipts"],
                    datasets: [{
                        data: [9276260, 730906, 1616184],
                        backgroundColor: ["#FF6384", "#36A2EB", "#FFCE56"],
                        hoverOffset: 10
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: {
                            position: "bottom",
                            labels: { color: "white" }
                        }
                    }
                }
            });
        });
    </script>
    
    <div class="folder" onclick="toggleFolder(this)">
        <h2>Tax Levy</h2>
        <div class="folder-content">
            <p>The tax levy is the primary revenue source for the town, including general taxation, annual increases under Prop 2.5%, new growth, and approved debt exclusions.</p>
            <table>
                <tr><th>Category</th><th>FY23</th><th>FY24</th><th>FY25</th><th>FY26 Proposed</th></tr>
                <tr><td>Tax Levy</td><td>$8,052,778</td><td>$8,425,343</td><td>$8,852,569</td><td>$9,276,260</td></tr>
                <tr><td>Prop 2.5%</td><td>$202,089</td><td>$210,633</td><td>$221,314</td><td>$230,000</td></tr>
                <tr><td>New Growth</td><td>$133,000</td><td>$134,215</td><td>$120,000</td><td>$140,000</td></tr>
                <tr><td>Debt Exclusions</td><td>$37,476</td><td>$82,377</td><td>$82,377</td><td>$85,000</td></tr>
            </table>
        </div>
    </div>
    
    <div class="folder" onclick="toggleFolder(this)">
        <h2>State Aid</h2>
        <div class="folder-content">
            <p>State aid includes unrestricted government assistance, reimbursements, and allocations for specific programs such as veterans' benefits and education offsets.</p>
            <table>
                <tr><th>Category</th><th>FY23</th><th>FY24</th><th>FY25</th><th>FY26 Proposed</th></tr>
                <tr><td>Unrestricted Aid</td><td>$521,806</td><td>$530,155</td><td>$554,659</td><td>$568,525</td></tr>
                <tr><td>Veterans' Benefits</td><td>$29,038</td><td>$24,861</td><td>$25,706</td><td>$26,348</td></tr>
            </table>
        </div>
    </div>
    
    <div class="folder" onclick="toggleFolder(this)">
        <h2>Local Receipts</h2>
        <div class="folder-content">
            <p>Local receipts capture revenue from excise taxes, licenses, permits, fines, service fees, and other locally generated income sources.</p>
            <table>
                <tr><th>Category</th><th>FY23</th><th>FY24</th><th>FY25</th><th>FY26 Proposed</th></tr>
                <tr><td>Motor Vehicle</td><td>$647,660</td><td>$716,352</td><td>$727,600</td><td>$778,532</td></tr>
                <tr><td>Building Permits</td><td>$47,750</td><td>$27,253</td><td>$50,000</td><td>$40,000</td></tr>
            </table>
        </div>
    </div>
    
    <script>
        function toggleFolder(folder) {
            let content = folder.querySelector(".folder-content");
            content.style.display = content.style.display === "block" ? "none" : "block";
        }
    </script>
</body>
</html>
