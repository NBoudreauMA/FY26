<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>FY26 Budget</title>
    
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
        .header {
            display: flex;
            flex-direction: column;
            align-items: center;
            margin-bottom: 20px;
        }
        .header img {
            width: 120px;
            margin-bottom: 10px;
        }
        h1 {
            color: #2d6a4f;
            font-size: 2.5rem;
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
    <div class="header">
        <img src="seal.png" alt="Town Seal">
        <h1>FY26 Budget</h1>
    </div>
    
    <!-- Navigation Buttons -->
    <div class="nav-container">
        <a href="expenditures.html" class="nav-button">Expenditures</a>
        <a href="revenue.html" class="nav-button">Revenue</a>
        <a href="summary.html" class="nav-button">Summary</a>
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
</body>
</html>
