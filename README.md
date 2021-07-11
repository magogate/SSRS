# SSRS (SQL Server Reporting Service)
# Videos
 1. SSRS - 1. Installation Prerequisite - https://youtu.be/bsV1yyv2Qe8
 2. SSRS - 2. Installation & Configuration of Sql Server Reporting Service - https://youtu.be/zavwVEYKoNw
 
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
    - Choose "Install Reporting Services"
    - Choose a free edition
    - Accepts license
    - Install Reporting Serices Only   
    - Install
    
### Configuring Report Server
 1. Connect to Node\SSRS
 2. **Service Account** -- Specify AD Account (gogates\SQL.PRD.SSRS) which we created earlier & Apply
 3. **Web Service URL** -- Keep default settings & Apply
 4. **Database** --
    - Click on Change database
    - Select - Create a new report server database
    - **Authentication Type** - Select "Integrated Security (Current User)
    - **Specify SQL Server** - GOGATE-NODE-1\DGOGATE
    - **Specify Database Name as Default** - ReportServer
    - **Credentials** -- Keep it default
    - Finish
 5. **Web Portal URL** -- Keep default
 6. Rest all settings are options and you can skip them
 7. Refresh the database, and you should be able to see new entries for ReportServer db
 8. Open - "Report Server Configuration Manager"
 9. Click on **Web Service URL** -- http://gogate-node-1/ReportServer
 10. It will prompt to specify user id & Password - specify required credentials **(gogates\magogate & P@ssword#123)**
 11. Click on **Web Portal URL** -- http://gogate-node-1/Reports/
 
### Download SQL Server Data Tools (SSDT) for Visual Studio
 1. In order to create SSRS reports, you need to have a client installed - and you can download that from (https://docs.microsoft.com/en-us/sql/ssdt/download-sql-server-data-tools-ssdt?view=sql-server-ver15#ssdt-for-vs-2017-standalone-installer)
 2. Once installation is finished, you can create a sample report by creating Report Service project using SSDT.
 3. You can deploy newly created report manually from http://gogate-node-1/Reports/
 

 
