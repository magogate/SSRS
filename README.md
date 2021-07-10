# SSRS (SQL Server Reporting Service)

# Intruduction
This video series we are going to see different types of SSRS reports along with Installation of SSRS on Windows machine.
## Installation of SQL Server Reporting Service
 1. Installation will be the very first step. I am going to use my old VMs which we had created at the time of SQL 2019 Cluster Configuration - you can find the repository at (https://github.com/magogate/SQL-2019-Active-Active-Cluster/edit/main/README.md)
 2. As we had created separate AD Accounts for SQL Agents and SQL Server services; for SSRS as well we are going to create new AD User - SQL.PRD.SSRS
 3. Prerequisite
    - Validate SQL Server Connection - if any services are down, start them from SQL Server Configuration Manager
    - You should be be able to connect with Windows Authentication since you are part of Domain Admin group.
    - Setup.exe --> Sql Server Intallation Center --> Install --> Install SQL Server Reporting Services (This needs Internet Access)
    - Check your internet connection. Add an additional NIC Card & select "Share IP Adderess of the Host"
    - Download chrome (its not mandatory but convenient)
 5. Once user creation is finished, we can start with actual SSSRS installation
    

