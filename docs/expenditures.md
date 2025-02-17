---
layout: default
title: "Budget Expenditures"
---

# 💸 Budget Expenditures

This page provides an overview of the expenditures for the Town of Hubbardston.

<table>
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
        {% for row in site.data.budget %}
        <tr>
            <td>{{ row.Department }}</td>
            <td>{{ row.Category }}</td>
            <td>${{ row.FY24 }}</td>
            <td>${{ row.FY25_Request }}</td>
            <td>${{ row.FY25 }}</td>
            <td>${{ row.FY26_Dept }}</td>
            <td>${{ row.FY26_Admin }}</td>
            <td>${{ row.Change_Dollar }}</td>
            <td>{{ row.Change_Percent }}%</td>
        </tr>
        {% endfor %}
    </tbody>
</table>
