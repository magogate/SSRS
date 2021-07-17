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
 
### Creating a dataset for Reporting
 1. You can use any data for reporting, but I am going to use HR schema which comes with Oracle DB installation by default for my convenience
 2. Once you install any Express Edition of Oracle, you just need to unlock the schema and change the password with below commands
    - alter user hr account unlock
    - alter user hr identified by P@ssword#123
 3. Or you can use SQL Navigator to perform these activities
 4. Once you logs into HR schema, export all table data int csv file
 5. Import those .csv files back into our SQL Server HR database
 
### Adding and Displaying Filters
 1. Once you add the filters, its important you display them at start of the report - because if you export the report and share it with others, she/he should know if the report is filtered report or not. 
 2. To display filters on SSRS reports, follow below steps
    - Add an expresssion just below the title and above your data table
    - Since filters which you are seeing on report are nothing but the parameters you have created. So, basically you are supposed to show those parameter values.
    - Since value parameters will get displayed on report without any issues
    - However, multivalue parameters (dropdowns with more than 1 values) - will throw an error. This is because - text box will expect an String, but multivalue parameters are collections / array. This needs to be type casted, so you can either use value(0) or label(0), but that's very ineffeciant way.
    - Instead, use join function. You can google - "how to convert array to string in ssrs expression" and you will get following URL
    - https://www.sqlshack.com/using-multi-value-parameters-in-ssrs/
    - Here, using JOIN function, you can convert Array into String, which can be displayed into SSRS
    - Also, if you are selecting all values in a drop down, there is no need to display each and every value. You can simple display "All Values Selected". however, how can we determine if all values in drop down are selected?
    - For that, you need to compare selected count vs count in database.
    - Count in database you will get from DataSet - so compare that with parameter count. If it matches then display "All Values" else display individual values.
    - Also, you may need to display these values on individual rows. for that you can use Chr(13) - this works in informatica as well - or Environment.NewLine
    - if you google - "how to add new line in ssrs expression" - you will come across link (https://stackoverflow.com/questions/22097129/line-break-in-ssrs-expression)
    - You can add <br> or <b> tag - which are HTML tag, but you need to select respective property for that - so SSRS will know to part HTML tags
    - 
 
  
