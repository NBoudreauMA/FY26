<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>FY26 Budget Expenditures</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f8f9fa;
            text-align: center;
            margin: 0;
        }
        h1, h2 {
            color: #5a2d82;
            margin-bottom: 5px;
        }
        .table-container {
            width: 98%;
            max-height: 75vh;
            overflow-y: auto;
            overflow-x: hidden;
            margin: 20px auto;
            border: 1px solid #ddd;
            background: white;
            padding-bottom: 10px;
        }
        table {
            width: 100%;
            border-collapse: collapse;
            background-color: white;
            table-layout: auto;
        }
        th, td {
            border: 1px solid #ddd;
            padding: 8px;
            text-align: left;
            vertical-align: middle;
            white-space: normal;
            word-wrap: break-word;
            font-size: 14px;
        }
        th {
            background-color: #5a2d82;
            color: white;
            font-weight: bold;
            position: sticky;
            top: 0;
            z-index: 2;
        }
        tr:nth-child(even) {
            background-color: #f2f2f2;
        }
        .error-message {
            color: red;
            font-weight: bold;
        }
    </style>
</head>
<body>
    <h1><a href="index.html" style="text-decoration: none; color: #5a2d82;">FY26</a></h1>
    <h2>FY26 Budget Expenditures</h2>
    <p>This page provides an overview of the expenditures for the Town of Hubbardston.</p>

    <div class="table-container">
        <table id="budgetTable">
            <thead>
                <tr>
                    <th style="width: 15%;">Department</th>
                    <th style="width: 12%;">Category</th>
                    <th style="width: 10%;">FY24</th>
                    <th style="width: 10%;">FY25 Request</th>
                    <th style="width: 10%;">FY25</th>
                    <th style="width: 10%;">FY26 Dept</th>
                    <th style="width: 10%;">FY26 Admin</th>
                    <th style="width: 10%;">Change ($)</th>
                    <th style="width: 10%;">Change (%)</th>
                </tr
