<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>FY26 Budget Expenditures</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 20px;
            background-color: #f8f9fa;
        }
        .container {
            max-width: 1200px;
            margin: 0 auto;
        }
        h1 {
            color: #5a2d82;
            text-align: center;
            margin-bottom: 1.5rem;
            font-size: 2rem;
        }
        .table-container {
            background: white;
            border-radius: 8px;
            box-shadow: 0 2px 4px rgba(0,0,0,0.1);
            overflow-x: auto;
        }
        table {
            width: 100%;
            border-collapse: collapse;
            margin: 0;
            table-layout: fixed;
        }
        th, td {
            padding: 12px;
            text-align: left;
            border: 1px solid #e2e8f0;
            word-wrap: break-word;
            overflow: hidden;
        }
        th {
            background-color: #5a2d82;
            color: white;
            font-weight: 600;
        }
        tr:nth-child(even) {
            background-color: #f8fafc;
        }
        td.number {
            text-align: right;
            font-family: 'Courier New', Courier, monospace;
        }
        .loading, .error {
            text-align: center;
            padding: 2rem;
            font-size: 1.1rem;
        }
        .error {
            color: #dc2626;
        }
        .total-row {
            background-color: #f3f0f5 !important;
            font-weight: 600;
        }
        thead {
            position: sticky;
            top: 0;
            background: #5a2d82;
            z-index: 2;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>FY26 Budget Expenditures</h1>
        <div class="table-container">
            <table id="budgetTable">
                <thead>
                    <tr>
                        <th>Department</th>
                        <th>Description</th>
                        <th>FY24</th>
