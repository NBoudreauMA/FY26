---
layout: default
title: Expenditures
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
    {% for item in site.data.budget.expenditures %}
    {% if item.Department and item.Department != "nan" %}
    <tr>
      <td>{{ item.Department }}</td>
      <td>{{ item.Category }}</td>
      <td>{{ item.FY24 }}</td>
      <td>{{ item.FY25_Request }}</td>
      <td>{{ item.FY25 }}</td>
      <td>{{ item.FY26_Dept }}</td>
      <td>{{ item.FY26_Admin }}</td>
      <td>{{ item.Change_Dollar }}</td>
      <td>{{ item.Change_Percent }}</td>
    </tr>
    {% endif %}
    {% endfor %}
  </tbody>
</table>
