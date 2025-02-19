import React from 'react';
import { PieChart, Pie, Cell, ResponsiveContainer } from 'recharts';
import { Card, CardHeader, CardTitle, CardContent } from '@/components/ui/card';

const BudgetPieChart = () => {
  const data = [ 
    { name: 'General Government', value: 731340.38 }, 
    { name: 'Public Safety', value: 1581842.23 }, 
    { name: 'Public Works', value: 920184.29 }, 
    { name: 'Education', value: 7294874.64 }, 
    { name: 'Human Services', value: 25550.00 }, 
    { name: 'Culture & Recreation', value: 94289.70 }, 
    { name: 'Debt', value: 146862.00 }, 
    { name: 'Liabilities & Assessments', value: 1004948.96 } 
  ];

  const COLORS = [
    '#2563eb', // Blue
    '#dc2626', // Red
    '#16a34a', // Green
    '#9333ea', // Purple
    '#ea580c', // Orange
    '#0d9488', // Teal
    '#db2777', // Pink
    '#854d0e'  // Brown
  ];

  const renderLabel = ({ cx, cy, midAngle, innerRadius, outerRadius, percent, name }) => {
    const RADIAN = Math.PI / 180;
    const radius = innerRadius + (outerRadius - innerRadius) * 1.2;
    const x = cx + radius * Math.cos(-midAngle * RADIAN);
    const y = cy + radius * Math.sin(-midAngle * RADIAN);

    return percent > 0.03 ? (
      <text
        x={x}
        y={y}
        fill="#374151"
        textAnchor={x > cx ? 'start' : 'end'}
        dominantBaseline="central"
        className="text-sm font-medium"
      >
        {`${name} (${(percent * 100).toFixed(1)}%)`}
      </text>
    ) : null;
  };

  return (
    <Card className="w-full">
      <CardHeader>
        <CardTitle>FY26 Proposed Budget Distribution</CardTitle>
      </CardHeader>
      <CardContent>
        <div className="h-96">
          <ResponsiveContainer width="100%" height="100%">
            <PieChart>
              <Pie
                data={data}
                cx="50%"
                cy="50%"
                outerRadius="65%"
                innerRadius="45%"
                dataKey="value"
                labelLine={true}
                label={renderLabel}
              >
                {data.map((entry, index) => (
                  <Cell key={`cell-${index}`} fill={COLORS[index % COLORS.length]} />
                ))}
              </Pie>
            </PieChart>
          </ResponsiveContainer>
        </div>
      </CardContent>
    </Card>
  );
};

export default BudgetPieChart;
    <title>FY26 Budget Expenditures</title>
    
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
            overflow-x: hidden;
        }
        h1 {
            color: #2d6a4f;
            font-size: 2.2rem;
        }
        .nav-container {
            margin-bottom: 10px;
        }
        .nav-container select {
            padding: 5px;
            font-size: 1rem;
            border: 1px solid #2d6a4f;
            border-radius: 5px;
        }
        .table-container {
            width: 100%;
            max-height: 90vh;
            overflow-y: auto;
            background: white;
            border-radius: 8px;
            padding: 10px;
            box-shadow: 0px 4px 6px rgba(0, 0, 0, 0.1);
        }
        table {
            width: 100%;
            border-collapse: collapse;
        }
        th, td {
            border: 1px solid #ddd;
            padding: 12px;
            text-align: left;
        }
        th {
            background-color: #2d6a4f;
            color: white;
            position: sticky;
            top: 0;
            z-index: 10;
        }
        tr:nth-child(even) {
            background-color: #f1f8f1;
        }
        td:first-child {
            font-weight: bold;
            background-color: #d4edda;
        }
    </style>
</head>
<body>
    <h1>FY26 Budget Expenditures</h1>
    
    <div class="nav-container">
        <label for="departmentDropdown">Jump To:</label>
        <select id="departmentDropdown" onchange="jumpToDepartment()">
            <option value="">Select...</option>
        </select>
    </div>
    
    <div class="table-container">
        <table id="budgetTable">
            <thead>
                <tr id="tableHeader"></tr>
            </thead>
            <tbody>
                <tr><td colspan="100%" class="error">Loading budget data...</td></tr>
            </tbody>
        </table>
    </div>
    
    <script>
        document.addEventListener("DOMContentLoaded", function () {
            loadBudgetData();
        });

        async function loadBudgetData() {
            const csvUrl = "https://raw.githubusercontent.com/NBoudreauMA/FY26/main/docs/budget2.csv";
            try {
                const response = await fetch(csvUrl);
                if (!response.ok) throw new Error("Failed to load CSV file. Ensure the URL is correct.");
                const data = await response.text();
                populateTable(data);
            } catch (error) {
                document.querySelector("#budgetTable tbody").innerHTML = `<tr><td colspan="100%">${error.message}</td></tr>`;
            }
        }

        function populateTable(csvText) {
            const tableHeader = document.querySelector("#tableHeader");
            const tableBody = document.querySelector("#budgetTable tbody");
            const dropdown = document.querySelector("#departmentDropdown");
            const rows = csvText.trim().split("\n").map(row => row.split(","));
            
            tableHeader.innerHTML = rows[0].map(header => `<th>${header.trim()}</th>`).join("");
            let tableContent = "";
            let departments = new Map();
            
            rows.slice(1).forEach((row, index) => {
                let department = row[0] ? row[0].trim() : "";
                let departmentId = `dept-${index}`;
                
                if (department && !departments.has(department)) {
                    departments.set(department, departmentId);
                    let option = document.createElement("option");
                    option.value = departmentId;
                    option.textContent = department;
                    dropdown.appendChild(option);
                    tableContent += `<tr id="${departmentId}" style="background-color:#d4edda; font-weight:bold;"><td colspan="100%">${department}</td></tr>`;
                }
                tableContent += "<tr>" + row.map(cell => `<td>${cell.trim()}</td>`).join("") + "</tr>";
            });
            tableBody.innerHTML = tableContent;
        }
        
        function jumpToDepartment() {
            const dropdown = document.querySelector("#departmentDropdown");
            const selectedDept = dropdown.value;
            if (selectedDept) {
                document.getElementById(selectedDept)?.scrollIntoView({ behavior: "smooth" });
            }
        }
    </script>
</body>
</html>
