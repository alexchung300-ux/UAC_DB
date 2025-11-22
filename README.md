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
<img width="532" height="423" alt="image" src="https://github.com/user-attachments/assets/e149942d-98f0-42e2-b704-9fc807e6e344" />


### Find all Users with a specific permission
<img width="524" height="251" alt="image" src="https://github.com/user-attachments/assets/10a1331a-9ab2-47e4-b3d5-d5b36780866f" />

### Recent access log activity
<img width="629" height="366" alt="image" src="https://github.com/user-attachments/assets/20a1b445-24ae-4edb-8856-66542dd9bc47" />

