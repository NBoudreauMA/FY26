<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Hubbardston Budget Portal</title>
    <link rel="stylesheet" href="assets/css/style.css">
    <style>
        /* General Reset */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: "Arial", sans-serif;
            scroll-behavior: smooth;
        }

        /* Full-Screen Background Image */
        body {
            background: url('assets/hubbardston_bg.jpg') no-repeat center center/cover;
            color: white;
            text-align: center;
            height: 100vh;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            position: relative;
        }

        /* Dark Overlay for Readability */
        body::before {
            content: "";
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.5);
            z-index: -1;
        }

        /* Transparent Logo Header */
        .header {
            position: absolute;
            top: 20px;
            left: 50%;
            transform: translateX(-50%);
            width: 150px;
            opacity: 0.9;
        }

        /* Navbar */
        .navbar {
            display: flex;
            gap: 20px;
            background: rgba(0, 0, 0, 0.6);
            padding: 15px 25px;
            border-radius: 10px;
            backdrop-filter: blur(10px);
            box-shadow: 0px 2px 10px rgba(0, 0, 0, 0.3);
        }

        .navbar a {
            color: white;
            text-decoration: none;
            font-weight: bold;
            padding: 8px 15px;
            border-radius: 5px;
            transition: 0.3s ease-in-out;
        }

        .navbar a:hover {
            background: rgba(255, 255, 255, 0.2);
        }

        /* Main Container */
        .container {
            max-width: 900px;
            padding: 40px;
            background: rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(10px);
            border-radius: 12px;
            box-shadow: 0px 5px 15px rgba(0, 0, 0, 0.2);
        }

        h1 {
            font-size: 36px;
            margin-bottom: 10px;
            color: #4CAF50; /* Green Theme */
        }

        p {
            font-size: 18px;
            line-height: 1.6;
            margin-bottom: 20px;
        }

        /* Quick Links */
        .quick-links {
            list-style: none;
            padding: 0;
        }

        .quick-links li {
            margin: 10px 0;
            padding: 12px;
            background: rgba(0, 0, 0, 0.4);
            border-radius: 5px;
            transition: 0.3s ease;
        }

        .quick-links li a {
            text-decoration: none;
            color: white;
            font-size: 18px;
            display: block;
        }

        .quick-links li:hover {
            background: rgba(255, 255, 255, 0.2);
        }

        /* Footer */
        .footer {
            position: absolute;
            bottom: 20px;
            font-size: 14px;
            background: rgba(0, 0, 0, 0.6);
            padding: 10px 20px;
            border-radius: 5px;
        }
    </style>
</head>
<body>

    <!-- Transparent Logo -->
    <img src="assets/Dedication_PH.png" alt="Hubbardston Seal" class="header">

    <!-- Navigation Bar -->
    <div class="navbar">
        <a href="index.html">🏠 Home</a>
        <a href="revenue.html">💰 Revenue</a>
        <a href="expenditures.html">💸 Expenditures</a>
        <a href="dashboard/index.html">📊 Dashboard</a>
    </div>

    <!-- Main Content -->
    <div class="container">
        <h1>Welcome to Hubbardston's Budget Portal</h1>
        <p>
            A **modern, interactive platform** designed to enhance **financial transparency** 
            and **community engagement** in Hubbardston.
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
