
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
