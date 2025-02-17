---
layout: default
title: Budget Expenditures
---

# 💸 Budget Expenditures

This page provides an overview of the expenditures for the Town of Hubbardston.

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
        <!-- Data will be inserted here -->
    </tbody>
</table>

<script>
    document.addEventListener("DOMContentLoaded", function () {
        fetch("assets/budget.csv")
            .then(response => response.text())
            .then(data => {
                const rows = data.split("\n").slice(1); // Skip the header row
                const tableBody = document.querySelector("#budget-table tbody");

                rows.forEach(row => {
                    const columns = row.split(",");
                    if (columns.length > 1) {
                        let tr = document.createElem
