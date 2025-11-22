# User Access Control Database

This project is a small role-based access control (RBAC) system built in MySQL. It includes tables for users, roles, permissions, role-permission assignments, user-role mappings, and access logs. The data is synthetic and was generated with the help of AI. The goal is to show that I can design a relational structure, populate it with realistic data, and analyze it using SQL.

## What’s Included
Core Tables

users – basic user information

roles – role names such as Admin or Manager

permissions – actions that can be granted

userroles – links users to one or more roles

rolepermissions – defines which permissions belong to each role

accesslogs – activity records for auditing

These tables work together to model a simple identity and access management system.

## Setup

Create a MySQL database

Run the table creation script

Insert the sample synthetic data

Use the provided queries to explore and test the system

Everything is lightweight and can run in any standard MySQL setup.

## Queries For Exploration

### List Users and their roles
<img width="486" height="316" alt="image" src="https://github.com/user-attachments/assets/cf73b27a-6392-4232-90b7-c95b886254f7" />


### Show each role with its permissions
mysql> SELECT r.role_name, p.permission_name
    -> FROM roles r
    -> JOIN rolepermissions rp ON r.role_id = rp.role_id
    -> JOIN permissions p ON rp.permission_id = p.permission_id;
+-----------+-----------------+
| role_name | permission_name |
+-----------+-----------------+
| Admin     | view_users      |
| Admin     | edit_users      |
| Admin     | delete_users    |
| Admin     | view_logs       |
| Admin     | manage_roles    |
| Admin     | assign_roles    |
| Admin     | view_reports    |
| Admin     | edit_reports    |
| Analyst   | view_users      |
| Analyst   | view_reports    |
| Intern    | view_users      |
| Manager   | view_users      |
| Manager   | edit_users      |
| Manager   | view_reports    |
| Manager   | edit_reports    |
| Support   | view_users      |
| Support   | view_logs       |
+-----------+-----------------+
17 rows in set (0.00 sec)

### Find all Users with a specific permission
mysql> SELECT u.username, p.permission_name
    -> FROM users u
    -> JOIN userroles ur ON u.user_id = ur.user_id
    -> JOIN roles r ON ur.role_id = r.role_id
    -> JOIN rolepermissions rp ON r.role_id = rp.role_id
    -> JOIN permissions p ON rp.permission_id = p.permission_id
    -> WHERE p.permission_name = 'edit_users';
+----------+-----------------+
| username | permission_name |
+----------+-----------------+
| jdoe     | edit_users      |
| asmith   | edit_users      |
| tjackson | edit_users      |
+----------+-----------------+
3 rows in set (0.00 sec)

### Recent access log activity
mysql> SELECT a.log_id, u.username, a.action, a.action_time
    -> FROM accesslogs a
    -> LEFT JOIN users u ON a.user_id = u.user_id
    -> ORDER BY a.action_time DESC
    -> LIMIT 25;
+--------+------------+-----------------------------+---------------------+
| log_id | username   | action                      | action_time         |
+--------+------------+-----------------------------+---------------------+
|     10 | ahernandez | Viewed analytics report     | 2025-11-22 16:17:28 |
|      9 | dclark     | Attempted restricted action | 2025-11-22 16:15:28 |
|      8 | bkim       | Viewed user profile         | 2025-11-22 16:12:28 |
|      7 | swhite     | Viewed logs                 | 2025-11-22 16:07:28 |
|      6 | tjackson   | Edited report               | 2025-11-22 15:47:28 |
|      5 | rlopez     | Viewed dashboard            | 2025-11-22 15:17:28 |
|      4 | kpatel     | Responded to support ticket | 2025-11-22 13:17:28 |
|      3 | mnguyen    | Viewed analytics report     | 2025-11-22 11:17:28 |
|      2 | asmith     | Viewed user list            | 2025-11-21 16:17:28 |
|      1 | jdoe       | Updated role permissions    | 2025-11-20 16:17:28 |
+--------+------------+-----------------------------+---------------------+
10 rows in set (0.00 sec)

