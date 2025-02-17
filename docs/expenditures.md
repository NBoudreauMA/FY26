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
    const csvURL = "{{ site.baseurl }}/docs/assets/budget.csv"; // Reference CSV file location

    const response = await fetch(csvURL);
    const data = await response.text();
    const rows = data.split("\n").map(row => row.split(","));

    const tableBody = document.querySelector("#budget-table tbody");
    tableBody.innerHTML = ""; // Clear existing content

    for (let i = 1; i < rows.length; i++) { // Skip header row
      const row = rows[i];
      if (row.length < 9) continue; // Ensure valid row length
      const tr = document.createElement("tr");
      row.forEach(cell => {
        const td = document.createElement("td");
        td.textContent = cell;
        tr.appendChild(td);
      });
      tableBody.appendChild(tr);
    }
  }

  loadBudgetData();
</script>
