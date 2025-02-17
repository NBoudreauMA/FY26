<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Hubbardston Budget Portal</title>

    <!-- Google Fonts for Modern Look -->
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600;700&display=swap" rel="stylesheet">
    
    <!-- Link to CSS -->
    <link rel="stylesheet" href="assets/css/style.css">

    <style>
        /* General Reset */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Inter', sans-serif; /* Modern Font */
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
            overflow: hidden;
        }

        /* Dark Overlay for Readability */
        body::before {
            content: "";
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.45);
            z-index: -1;
        }

        /* Transparent Logo Header */
        .header {
            position: absolute;
            top: 25px;
            left: 50%;
            transform: translateX(-50%);
            width: 140px;
            opacity: 0.95;
            filter: drop-shadow(0px 0px 6px rgba(255, 255, 255, 0.3));
        }

        /* Main Title */
        .title {
            font-size: 38px;
            font-weight: 700;
            letter-spacing: 1px;
            color: #4CAF50; /* Green Theme */
            text-shadow: 2px 2px 10px rgba(0, 0, 0, 0.8);
            margin-bottom: 15px;
        }

        /* Navigation Bar */
        .navbar {
            display: flex;
            gap: 18px;
            background: rgba(0, 0, 0, 0.65);
            padding: 10px 28px;
            border-radius: 10px;
            backdrop-filter: blur(8px);
            box-shadow: 0px 2px 8px rgba(0, 0, 0, 0.2);
            transition: 0.3s ease-in-out;
        }

        .navbar a {
            color: white;
            text-decoration: none;
            font-weight: 600;
            font-size: 15px;
            padding: 8px 15px;
            border-radius: 6px;
            transition: 0.3s ease-in-out;
        }

        .navbar a:hover {
            background: rgba(255, 255, 255, 0.2);
        }

        /* Main Container */
        .container {
            max-width: 750px;
            padding: 30px;
            background: rgba(255, 255, 255, 0.15);
            backdrop-filter: blur(10px);
            border-radius: 12px;
            box-shadow: 0px 5px 12px rgba(0, 0, 0, 0.2);
            animation: fadeIn 1s ease-in-out;
        }

        /* Quick Links */
        .quick-links {
            list-style: none;
            padding: 0;
        }

        .quick-links li {
            margin: 10px 0;
            padding: 12px;
            background: rgba(0, 0, 0, 0.35);
            border-radius: 8px;
            transition: 0.3s ease;
        }

        .quick-links li a {
            text-decoration: none;
            color: white;
            font-size: 16px;
            font-weight: 600;
            display: block;
        }

        .quick-links li:hover {
            background: rgba(255, 255, 255, 0.25);
        }

        /* Footer */
        .footer {
            position: absolute;
            bottom: 12px;
            font-size: 14px;
            background: rgba(0, 0, 0, 0.6);
            padding: 8px 18px;
            border-radius: 8px;
            font-weight: 400;
        }

        /* Fade-in Effect */
        @keyframes fadeIn {
            from {
                opacity: 0;
                transform: translateY(-8px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
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
        <h1 class="title">Welcome to Hubbardston's Budget Portal</h1>
        <p style="font-size: 17px; font-weight: 400;">
            A <strong>modern, interactive platform</strong> designed to enhance <strong>financial transparency</strong> 
            and <strong>community engagement</strong> in Hubbardston.
        </p>

        <h2 style="margin-top: 15px;">📂 Quick Links</h2>
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
