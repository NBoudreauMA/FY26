<script>
    async function loadBudgetData() {
        const csvUrl = "https://raw.githubusercontent.com/NBoudreauMA/FY26/main/docs/budget.csv"; // Update with correct CSV link

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
        const rows = csvText.trim().split("\n").map(row => row.split(","));
        let tableBody = "";
        let departmentData = [];
        let expenseData = [];

        rows.slice(1).forEach(row => {
            if (row.length > 1) {
                tableBody += "<tr>";
                let department = "";
                let fy26AdminValue = 0;

                row.forEach((cell, index) => {
                    let cellValue = cell.trim();

                    // Fix Department & Category Spacing
                    if (index === 0 || index === 1) {
                        cellValue = cellValue
                            .replace(/([a-z])([A-Z])/g, '$1 $2') // Add space in camelCase text
                            .replace(/([0-9])([A-Za-z])/g, '$1 $2') // Add space between numbers and words
                            .replace(/([A-Za-z])([0-9])/g, '$1 $2') // Add space between words and numbers
                            .replace(/([A-Z])([A-Z][a-z])/g, '$1 $2') // Add space between uppercase acronyms & names
                            .replace(/[-_]/g, " "); // Ensure hyphenated and underscored words are properly spaced
                    }

                    // Fix Number Formatting: Remove spaces inside numbers & ensure correct commas
                    cellValue = cellValue.replace(/"|\s(?=\d)/g, "");  // Remove extra spaces & quotes

                    // Convert numeric values correctly
                    if (!isNaN(cellValue) && cellValue !== "" && cellValue.length > 0) {
                        cellValue = parseFloat(cellValue.replace(/,/g, '')).toLocaleString(); // Format as number with commas
                    }

                    if (index === 0) department = cellValue; // Store department name
                    if (index === 6 && !isNaN(cellValue.replace(/,/g, ''))) {
                        fy26AdminValue = parseFloat(cellValue.replace(/,/g, '')); // Store FY26 Admin expenses
                    }

                    tableBody += `<td>${cellValue}</td>`;
                });
                tableBody += "</tr>";

                // Add data to chart arrays
                if (department && fy26AdminValue > 0) {
                    departmentData.push(department);
                    expenseData.push(fy26AdminValue);
                }
            }
        });

        document.querySelector("#budgetTable tbody").innerHTML = tableBody;
    }

    loadBudgetData();
</script>
