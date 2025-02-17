<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Hubbardston Budget</title>
    <link rel="stylesheet" href="assets/css/style.css">
    <style>
        /* General Reset */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: "Arial", sans-serif;
        }

        body {
            background-color: #f8f9fa;
            color: #2c3e50;
            text-align: center;
        }

        /* Header */
        .header {
            background: url('assets/Dedication_PH.jpg') no-repeat center;
            background-size: contain;
            height: 150px;
        }

        /* Navbar */
        .navbar {
            display: flex;
            justify-content: center;
            background-color: #004d00;
            padding: 15px;
            box-shadow: 0px 2px 10px rgba(0, 0, 0, 0.2);
        }

        .navbar a {
            color: white;
            text-decoration: none;
            padding: 10px 20px;
            font-weight: bold;
            transition: 0.3s ease-in-out;
        }

        .navbar a:hover {
            background: #006400;
            border-radius: 5px;
        }

        /* Main Container */
        .container {
            max-width: 900px;
            margin: 40px auto;
            background: white;
            padding: 30px;
            border-radius: 8px;
            box-shadow: 0px 5px 15px rgba(0, 0, 0, 0.1);
        }

        h1 {
            font-size: 28px;
            color: #004d00;
            margin-bottom: 15px;
        }

        p {
            font-size: 18px;
            line-height: 1.6;
        }

        /* Quick Links */
        .quick-links {
            list-style: none;
            padding: 0;
        }

        .quick-links li {
            background: #004d00;
            margin: 10px 0;
            border-radius: 5px;
            padding: 12px;
            transition: 0.3s ease;
        }

        .quick-links li a {
            text-decoration: none;
            color: white;
            font-size: 18px;
            display: block;
        }

        .quick-links li:hover {
            background: #006400;
        }

        /* Footer */
        .footer {
            background: #002800;
            color: white;
            padding: 15px;
            font-size: 14px;
            margin-top: 30px;
        }
    </style>
</head>
<body>
    <!-- Header with Hubbardston Seal -->
    <div class="header"></div>

    <!-- Navigation Bar -->
    <div class="navbar">
        <a href="index.html">🏠 Home</a>
        <a href="revenue.html">💰 Revenue</a>
        <a href="expenditures.html">💸 Expenditures</a>
        <a href="dashboard/index.html">📊 Dashboard</a>
    </div>

    <!-- Main Content -->
    <div class="container">
        <h1>Welcome to the Interactive Budget</h1>
        <p>
            This platform enhances **budget transparency and accessibility** for the residents of Hubbardston.
            Explore the town’s financials with a **modern, easy-to-navigate dashboard**.
        </p>

        <h2>📂 Quick Links</h2>
        <ul class="quick-links">
            <li><a href="revenue.html">💰 View Revenue Details</a></li>
            <li><a href="expenditures.html">💸 View Expenditures</a></li>
            <li><a href="dashboard/index.html">📊 Explore Budget Dashboard</a></li>
        </ul>
    </div>

    <!-- Footer -->
    <div class="footer">
        &copy; 2025 Town of Hubbardston | All Rights Reserved
    </div>
</body>
</html>
