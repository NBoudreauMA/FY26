<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>FY26 Budget Overview</title>

    <!-- Google Fonts & Styling -->
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600&display=swap" rel="stylesheet">
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
        }
        h1 {
            color: #2d6a4f;
            font-size: 2.5rem;
            margin-bottom: 10px;
        }
        .subtitle {
            color: #555;
            font-size: 1.2rem;
            margin-bottom: 20px;
        }
        .nav-container {
            display: flex;
            justify-content: center;
            flex-wrap: wrap;
            gap: 15px;
            margin-top: 20px;
        }
        .nav-button {
            background-color: #2d6a4f;
            color: white;
            font-size: 1rem;
            padding: 12px 20px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            text-decoration: none;
            transition: background 0.3s ease;
        }
        .nav-button:hover {
            background-color: #1e4e36;
        }
        .content-box {
            background: white;
            border-radius: 8px;
            padding: 20px;
            box-shadow: 0px 4px 6px rgba(0, 0, 0, 0.1);
            max-width: 900px;
            margin: 20px auto;
            text-align: left;
        }
        .content-box h2 {
            color: #2d6a4f;
            font-size: 1.5rem;
            margin-bottom: 10px;
        }
        .content-box p {
            color: #333;
            line-height: 1.6;
            font-size: 1rem;
        }
    </style>
</head>
<body>
    <h1>FY26 Budget Overview</h1>
    <p class="subtitle">A transparent, detailed look at the fiscal year 2026 budget.</p>

    <!-- Navigation Buttons -->
    <div class="nav-container">
        <a href="expenditures.html" class="nav-button">View Expenditures</a>
        <a href="revenue.html" class="nav-button">View Revenue</a>
        <a href="summary.html" class="nav-button">Budget Summary</a>
    </div>

    <!-- Content Box -->
    <div class="content-box">
        <h2>About This Budget</h2>
        <p>
            The FY26 budget represents a balanced, strategic plan for resource allocation,
            prioritizing essential services, infrastructure improvements, and community initiatives.
            This platform provides transparency, allowing residents to explore expenditures and revenue sources in detail.
        </p>
    </div>

    <div class="content-box">
        <h2>How to Use This Platform</h2>
        <p>
            Navigate through the different sections using the buttons above. The "Expenditures" section
            details departmental spending, while "Revenue" provides insight into funding sources. The
            "Summary" section offers a high-level breakdown of key financial metrics.
        </p>
    </div>
</body>
</html>
