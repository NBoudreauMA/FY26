<script>
    async function loadBudgetData() {
        const csvUrl = "https://raw.githubusercontent.com/NBoudreauMA/FY26/main/docs/budget.csv";

        try {
            const response = await fetch(csvUrl);
            if (!response.ok) throw new Error("Failed to load CSV file. Ensure the URL is correct.");
            const data = await response.text();
            populateTable(data);
        } catch (error) {
            document.querySelector("#budgetTable tbody").innerHTML = `<tr><td colspan="9" class="error">${error.message}</td></tr>`;
        }
    }

    function populateTable(csvText) {
        const tableBody = document.querySelector("#budgetTable tbody");
        if (!tableBody) {
            console.error("Table not found in expenditures.html.");
            return;
        }

        const rows = csvText.trim().split("\n").map(row => row.split(","));
        let tableContent = "";
        let departmentData = [];
        let expenseData = [];

        rows.slice(1).forEach(row => {
            if (row.length > 1) {
                tableContent += "<tr>";
                let department = "";
                let fy26AdminValue = 0;

                row.forEach((cell, index) => {
                    let cellValue = cell.trim();

                    // ✅ Fix Department & Category Spacing
                    if (index === 0 || index === 1) {
                        cellValue = cellValue
                            .replace(/([a-z])([A-Z])/g, '$1 $2') 
                            .replace(/([0-9])([A-Za-z])/g, '$1 $2') 
                            .replace(/([A-Za-z])([0-9])/g, '$1 $2') 
                            .replace(/([A-Z])([A-Z][a-z])/g, '$1 $2') 
                            .replace(/[-_]/g, " ");
                    }

                    // ✅ Fix Number Formatting: Remove spaces inside numbers
                    cellValue = cellValue.replace(/\s(?=\d)/g, "");

                    // ✅ Convert numeric values correctly
                    if (!isNaN(cellValue) && cellValue !== "") {
                        cellValue = parseFloat(cellValue.replace(/,/g, '')).toLocaleString();
                    }

                    if (index === 0) department = cellValue;
                    if (index === 6 && !isNaN(cellValue.replace(/,/g, ''))) {
                        fy26AdminValue = parseFloat(cellValue.replace(/,/g, ''));
                    }

                    tableContent += `<td>${cellValue}</td>`;
                });
                tableContent += "</tr>";

                if (department && fy26AdminValue > 0) {
                    departmentData.push(department);
                    expenseData.push(fy26AdminValue);
                }
            }
        });

        tableBody.innerHTML = tableContent;
        drawChart(departmentData, expenseData);
    }

    function drawChart(labels, data) {
        const ctx = document.getElementById("budgetChart").getContext("2d");

        new Chart(ctx, {
            type: "bar",
            data: {
                labels: labels,
                datasets: [{
                    label: "FY26 Admin Expenditures",
                    data: data,
                    backgroundColor: "rgba(90, 45, 130, 0.7)",
                    borderColor: "rgba(90, 45, 130, 1)",
                    borderWidth: 1
                }]
            },
            options: {
                responsive: true,
                scales: {
                    y: {
                        beginAtZero: true
                    }
                }
            }
        });
    }

    document.addEventListener("DOMContentLoaded", loadBudgetData);
</script>
