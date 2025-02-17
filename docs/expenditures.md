<script>
    async function loadBudgetData() {
        const csvUrl = "https://raw.githubusercontent.com/NBoudreauMA/FY26/main/docs/budget.csv"; // Ensure the correct URL

        try {
            const response = await fetch(csvUrl);
            if (!response.ok) throw new Error("Failed to load CSV file. Ensure the URL is correct.");

            const data = await response.text();
            populateTable(data);
        } catch (error) {
            const tableBody = document.querySelector("#budgetTable tbody");
            if (tableBody) {
                tableBody.innerHTML = `<tr><td colspan="9" class="error">${error.message}</td></tr>`;
            } else {
                console.error("Table not found. Ensure the HTML contains the correct table structure.");
            }
        }
    }

    function populateTable(csvText) {
        const tableBody = document.querySelector("#budgetTable tbody");
        if (!tableBody) {
            console.error("Table not found in the document.");
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

                    // Fix Department & Category Spacing
                    if (index === 0 || index === 1) {
                        cellValue = cellValue
                            .replace(/([a-z])([A-Z])/g, '$1 $2') // Add space in camelCase text
                            .replace(/([0-9])([A-Za-z])/g, '$1 $2') // Add space between numbers and words
                            .replace(/([A-Za-z])([0-9])/g, '$1 $2') // Add space between words and numbers
                            .replace(/([A-Z])([A-Z][a-z])/g, '$1 $2') // Add space between uppercase acronyms & names
                            .replace(/[-_]/g, " "); // Ensure hyphenated words are properly spaced
                    }

                    // Fix Number Formatting: Remove spaces inside numbers & format them properly
                    cellValue = cellValue.replace(/"|\s(?=\d)/g, "");  // Remove extra spaces & quotes

                    // Convert numeric values correctly
                    if (!isNaN(cellValue) && cellValue !== "") {
                        cellValue = parseFloat(cellValue.replace(/,/g, '')).toLocaleString(); // Format with commas
                    }

                    if (index === 0) department = cellValue;
                    if (index === 6 && !isNaN(cellValue.replace(/,/g, ''))) {
                        fy26AdminValue = parseFloat(cellValue.replace(/,/g, ''));
                    }

                    tableContent += `<td>${cellValue}</td>`;
                });
                tableContent += "</tr>";

                // Add data to chart arrays
                if (department && fy26AdminValue > 0) {
                    departmentData.push(department);
                    expenseData.push(fy26AdminValue);
                }
            }
        });

        tableBody.innerHTML = tableContent;
    }

    document.addEventListener("DOMContentLoaded", () => {
        if (!document.querySelector("#budgetTable")) {
            console.error("Table is missing from the HTML. Ensure the table exists.");
            return;
        }
        loadBudgetData();
    });
</script>
