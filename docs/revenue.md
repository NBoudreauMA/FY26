<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>FY26 Revenue</title>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <link rel="stylesheet" href="assets/css/style.css">
</head>
<body>
    <h1>FY26 Hubbardston Revenue Breakdown</h1>
    
    <div class="chart-container">
        <canvas id="revenueChart"></canvas>
    </div>

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
                    maintainAspectRatio: false
                }
            });
        });
    </script>
</body>
</html>
