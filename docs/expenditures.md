---
layout: default
title: Expenditures
---

# 📊 Expenditures Summary
This page provides an overview of the expenditures for the Town of Hubbardston.

## 💰 Budget Expenditures

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
    {% if item.Department and item.Department != ".nan" %} <!-- Filter out invalid rows -->
    <tr>
      <td>{{ item.Department }}</td>
      <td>{{ item.Category }}</td>
      <td>{{ item.FY24 }}</td>
      <td>{{ item.FY25_Request }}</td>
      <td>{{ item.FY25 }}</td>
      <td>{{ item.FY26_Dept }}</td>
      <td>{{ item.FY26_Admin }}</td>
      <td class="{% if item.Change_Dollar contains '-' %}negative{% else %}positive{% endif %}">
          ${{ item.Change_Dollar }}
      </td>
      <td class="{% if item.Change_Percent contains '-' %}negative{% else %}positive{% endif %}">
          {{ item.Change_Percent }}
      </td>
    </tr>
    {% endif %}
    {% endfor %}
  </tbody>
</table>
