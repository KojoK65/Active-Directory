# 🛠️ Active Directory Lab

This lab demonstrates how PowerShell can be used to automate Active Directory user provisioning tasks. It includes the creation of a single user, importing multiple users from a CSV file, and verifying the results within Active Directory Users & Computers (ADUC).

---

## ✅ Objective

Showcase how to automate user account creation and management in Active Directory using PowerShell scripting and CSV-based input.

---

## 🧰 Lab Environment

- **PowerShell ISE** (Run as Administrator)
- **Active Directory Module for Windows PowerShell**
- **Windows Server 2019 VM** with AD DS installed
- **Active Directory Users & Computers (ADUC)** GUI

---

## 🧪 Step 1: Create a Single User Manually Using PowerShell

Created a user account named `ron` with specific attributes, set a password, and enabled the account.

### 🔹 Script Used:
```powershell
# Create a new user with attributes
New-ADUser ron -Office Boston -Company Atlantis -MobilePhone "(123)987-4254"

# View all properties for the user
Get-ADUser ron -Property *

# Set a password and enable the account
$pw = Read-Host "What is the password" -AsSecureString
Set-ADAccountPassword ron -NewPassword $pw
Enable-ADAccount ron
# Active-Directory

```
## Creating the user ron in PowerShell
<img width="1280" alt="ss#1" src="https://github.com/user-attachments/assets/e8d8042b-5843-455f-a4ee-9599666c3dd1" />

# 🧪 Step 2: Bulk Import Users into Active Directory from CSV

Used a CSV file to bulk create multiple user accounts with attributes like name, department, title, and email. Each account is set to be **enabled** and required to **change the password on next login**.

---

## ✅ CSV File Location

Ensure `users.csv` is saved at:

C:\PS 2\users.csv
## 📄 `users.csv` Content

| samaccountname | name      | givenname | surname | displayname     | department | officephone    | city     | state |
|----------------|-----------|-----------|---------|------------------|------------|----------------|----------|-------|
| TBrady         | TBrady    | Tom       | Brady   | Tom Brady        | HR         | (616)458-6511  | Boston   | MA    |
| PManning       | PManning  | Peyton    | Manning | Peyton Manning   | HR         | (616)123-6547  | Denver   | CO    |
| RWilson        | RWilson   | Russell   | Wilson  | Russell Wilson   | HR         | (616)789-4972  | Seattle  | WA    |
| BMayfield      | BMayfield | Baker     | Mayfield| Baker Mayfield   | HR         | (616)467-1947  | Cleveland| OH    |



```# Preview users from CSV
Import-Csv ".\users.csv" | Out-GridView

# Basic bulk import using single-line command
Import-Csv ".\users.csv" | New-ADUser `
    -AccountPassword $(ConvertTo-SecureString "P@55w0rd" -AsPlainText -Force) `
    -ChangePasswordAtLogon $true `
    -Enabled $true

# Alternative import method with formatting
Import-Csv ".\users.csv" |
    New-ADUser 
        -Enabled $true 
        -AccountPassword $(ConvertTo-SecureString "Pa55w.rd" -AsPlainText -Force) 

    <img width="1280" alt="ss#2" src="https://github.com/user-attachments/assets/a6ea17b4-7b9f-4dfe-a2dd-7f8a7665ecbc" />
```

<img width="1280" alt="ss#2" src="https://github.com/user-attachments/assets/c8b3d18b-6a52-4404-bec3-8b0837d1fbde" />

## 🎯 Results

- ✅ Created a user manually using PowerShell  
- ✅ Imported a set of users from a structured CSV file  
- ✅ Confirmed creation and status of user accounts in **Active Directory Users and Computers (ADUC)**  
- ✅ Applied real-world parameters like titles, departments, and email addresses  
- ✅ All accounts enabled and set to prompt for password change at next login  

## 🚀 Summary

This lab demonstrates how to use PowerShell to automate user account management in an Active Directory environment. It covers the creation of individual users with specified attributes, setting and securing passwords, enabling accounts, and bulk provisioning users from a CSV file.

Each task mirrors typical administrative actions in a Windows domain, emphasizing **accuracy** and **repeatability** through scripting. The use of both manual and CSV-driven workflows shows how to manage identities efficiently at scale. Final verification using **Active Directory Users & Computers (ADUC)** confirms successful execution and account configuration.

This lab provides a practical baseline for scripting directory tasks and building repeatable processes in domain management.

