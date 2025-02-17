---
layout: default
title: Expenditures
---

# 💸 Budget Expenditures

This page provides an overview of the expenditures for the Town of Hubbardston.

<table id="budget-table">
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
  <tbody></tbody>
</table>

<script>
  async function loadBudgetData() {
    const csvURL = "{{ site.baseurl }}/docs/assets/budget.csv";
    console.log("Fetching CSV from:", csvURL); // Debugging: Check URL

    try {
      const response = await fetch(csvURL);
      if (!response.ok) throw new Error("CSV file not found");

      const data = await response.text();
      console.log("CSV Data Loaded:", data); // Debugging: Print CSV content

      const rows = data.split("\n").map(row => row.split(","));
      const tableBody = document.querySelector("#budget-table tbody");
      tableBody.innerHTML = ""; 

      for (let i = 1; i < rows.length; i++) { // Skip header row
        const row = rows[i];
        if (row.length < 9) continue;

        const tr = document.createElement("tr");
        row.forEach(cell => {
          const td = document.createElement("td");
          td.textContent = cell;
          tr.appendChild(td);
        });
        tableBody.appendChild(tr);
      }
    } catch (error) {
      console.error("Error loading CSV:", error);
    }
  }

  loadBudgetData();
</script>
