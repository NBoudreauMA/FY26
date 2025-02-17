<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Hubbardston Budget Portal</title>
    
    <!-- Google Fonts -->
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600&display=swap" rel="stylesheet">

    <style>
        /* Global Reset */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Inter', sans-serif;
        }

        /* Background Image */
        body {
            background: url('assets/hubbardston-ma-2.jpg') no-repeat center center fixed;
            background-size: cover;
            position: relative;
            color: #ffffff;
            text-align: center;
        }

        /* Overlay for readability */
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

        /* Header */
        header {
            padding: 20px;
            text-align: center;
        }

        .seal-logo {
            max-width: 120px;
            display: block;
            margin: 0 auto;
            filter: drop-shadow(2px 2px 5px rgba(0, 0, 0, 0.3));
        }

        h1 {
            font-size: 2.2rem;
            font-weight: 600;
            margin-top: 10px;
        }

        /* Navbar */
        nav {
            background: rgba(0, 0, 0, 0.7);
            padding: 10px;
            border-radius: 10px;
            display: inline-block;
            margin: 10px auto;
        }

        nav a {
            color: #fff;
            text-decoration: none;
            padding: 10px 20px;
            display: inline-block;
            transition: 0.3s;
            font-weight: 600;
        }

        nav a:hover {
            color: #ffd700;
        }

        /* Main Content */
        .content {
            padding: 50px;
        }

        h2 {
            font-size: 2rem;
            font-weight: 600;
            margin-bottom: 10px;
        }

        p {
            font-size: 1.2rem;
            font-weight: 300;
            max-width: 600px;
            margin: 0 auto 20px;
        }

        /* Quick Links */
        .quick-links {
            display: flex;
            justify-content: center;
            gap: 20px;
            margin-top: 20px;
        }

        .btn {
            background: rgba(255, 255, 255, 0.1);
            color: #fff;
            text-decoration: none;
            padding: 12px 20px;
            border-radius: 8px;
            border: 2px solid #fff;
            transition: 0.3s;
            font-weight: 600;
        }

        .btn:hover {
            background: #ffd700;
            color: #000;
            border: 2px solid #ffd700;
        }

        /* Footer */
        footer {
            margin-top: 50px;
            padding: 10px;
            background: rgba(0, 0, 0, 0.7);
            font-size: 0.9rem;
        }
    </style>
</head>
<body>

    <!-- Header Section -->
    <header>
        <img src="assets/seal.png" alt="Hubbardston Seal" class="seal-logo">
        <h1>FY26 Hubbardston Budget Portal</h1>
    </header>

    <!-- Navigation Bar -->
    <nav>
        <a href="index.html">🏠 Home</a>
        <a href="revenue.html">💰 Revenue</a>
        <a href="expenditures.html">💸 Expenditures</a>
        <a href="dashboard/index.html">📊 Dashboard</a>
    </nav>

    <!-- Main Content -->
    <div class="content">
        <h2>Welcome to Hubbardston's Budget Portal</h2>
        <p>A <strong>modern, interactive platform</strong> designed to enhance <strong>financial transparency</strong> and <strong>community engagement</strong> in Hubbardston.</p>

        <div class="quick-links">
            <a href="revenue.html" class="btn">💰 View Revenue Details</a>
            <a href="expenditures.html" class="btn">💸 View Expenditures</a>
            <a href="dashboard/index.html" class="btn">📊 Explore Budget Dashboard</a>
        </div>
    </div>

    <!-- Footer -->
    <footer>
        &copy; 2025 Town of Hubbardston | All Rights Reserved
    </footer>

</body>
</html>
