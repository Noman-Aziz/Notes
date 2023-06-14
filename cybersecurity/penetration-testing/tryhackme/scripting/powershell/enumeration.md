# Enumeration

### Introduction

The first step when you have gained initial access to any machine would be to enumerate

***

### Get Number of Users on a Machine

```powershell
Get-LocalUser
```

***

### Get Number of Local Groups

```powershell
Get-LocalGroup
```

***

### Get IP Address

```powershell
Get-NetIPAddress
```

***

### See Applied Patches

```powershell
Get-Hotfix
```

***

### Search for all files containing Specific Content

```powershell
Get-ChildItem C:\* -Recurse | Select-String -pattern SpecificContent
```

***

### Get list of Running Processes

```powershell
Get-Process
```

***

### Get list of Scheduled Tasks

```powershell
Get-ScheduleTask
```

***

### Check Owner of a Folder/File

```powershell
Get-Acl c:/
```

***
