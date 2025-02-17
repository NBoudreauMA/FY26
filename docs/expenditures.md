<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Budget Expenditures</title>
    <link rel="stylesheet" href="assets/css/style.css">
    <script src="https://cdnjs.cloudflare.com/ajax/libs/PapaParse/5.3.0/papaparse.min.js"></script>
</head>
<body>

    <h1>Budget Expenditures</h1>
    <p>This page provides an overview of the expenditures for the Town of Hubbardston.</p>

    <table id="budget-table" border="1">
        <thead>
            <tr>
                <th>Department</th>
                <th>Category</th>
                <th>FY24</th>
                <th>FY25 Request</th>
                <th>FY25</th>
                <th>FY26 Dept</th>
                <th>FY26 Admin</th>
                <th>Change ($)</th>
                <th>Change (%)</th>
            </tr>
        </thead>
        <tbody>
        </tbody>
    </table>

    <script>
        // Function to fetch and display CSV data
        function loadCSV() {
            fetch('assets/budget.csv')  // Ensure the path is correct
                .then(response => response.text())
                .then(csvText => {
                    Papa.parse(csvText, {
                        header: true,
                        skipEmptyLines: true,
                        complete: function(results) {
                            let tableBody = document.querySelector("#budget-table tbody");
                            results.data.forEach(row => {
                                let tr = document.createElement("tr");
                                tr.innerHTML = `
                                    <td>${row.Department || ''}</td>
                                    <td>${row.Category || ''}</td>
                                    <td>${row.FY24 || ''}</td>
                                    <td>${row.FY25_Request || ''}</td>
                                    <td>${row.FY25 || ''}</td>
                                    <td>${row.FY26_Dept || ''}</td>
                                    <td>${row.FY26_Admin || ''}</td>
                                    <td>${row["Change ($)"] || ''}</td>
                                    <td>${row["Change (%)"] || ''}</td>
                                `;
                                tableBody.appendChild(tr);
                            });
                        }
                    });
                })
                .catch(error => console.error("Error loading CSV:", error));
        }

        // Load CSV when the page loads
        window.onload = loadCSV;
    </script>

</body>
</html>
