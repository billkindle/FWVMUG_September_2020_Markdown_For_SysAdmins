# Adding a PowerShell Scheduled Job

## Description

This process outlines the steps required to setup a *Scheduled Job* using **PowerShell**. 
We use scheduled jobs as part of many maintenance processes performed by the team daily.
It will be beneficial for you to keep this document handy as a **Jr. Systems Administrator**. 

### Pre-Op Checklist

- Verify the maintenance window has been approved by change control board.
- Verify that notifications have been sent to stakeholders.
- Verify that you have the proper access to systems affected.

**If all of the above criteria has been met, proceed with configuring the PowerShell Scheduled Job**.

| Scheduled Time | Job Name | User Account | Will Email Be Sent? |
|---|---|---|---|
| 09:00 PM EDT | Stop IIS Services | SYSTEM | Yes |
| 09:30 PM EDT | Release WSUS Updates / Deadline | SYSTEM | No |
| 11:00 PM EDT | Start IIS Services | SYSTEM | Yes |

## Steps to Add Scheduled Job

Execute the following steps to add a PowerShell scheduled job:

1. Open Windows PowerShell
2. Enter the following command and press **Enter**: 
```powershell
    $O = New-ScheduledJobOption -WakeToRun -StartIfIdle -MultipleInstancePolicy Queue
    $T = New-JobTrigger -Weekly -At "9:00 PM" -DaysOfWeek Monday
    $path = "\\Srv01\Scripts\Stop-IISServices.ps1"
    Register-ScheduledJob -Name "UpdateVersion" -FilePath $path -ScheduledJobOption $O -Trigger $T
```

3. Verify scheduled job is active using Get-ScheduledJob and inspecting the list of jobs.
4. Notify Sr. Systesm Administrator that task is complete.

![alt_text](https://happyologist.co.uk/wp-content/uploads/happy.jpeg)