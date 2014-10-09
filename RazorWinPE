	#Prepare for Windows PE for Puppet Razor

##Prerequisites
	*A Clean Microsoft Windows PC running Windows 7 or Higher
	*Windows ADK
	*

##Assumptions
This document has the following assumptions

##Setup the folder structure
Create the following directories
	
	mkdir c:\build-winpe
	mkdir c:\build-winpe\razor-winpe
	mkdir C:\build-winpe\offline

##Download and Install the ADK Kit from Microsoft
You need to download the ADK from the Microsoft website, if the following URL does not work be assured that you should be able to search for it on the internet as this is an integral part of deploying Windows in an enterprise fashion.

http://www.microsoft.com/en-us/download/details.aspx?id=30652

##Create a working copy of winpe.wim
cd \Program Files (x86)\Windows Kits\8.0\Assesment and Deployment Kit\Windows Preinstallation Environment\amd64\

## Mount the WinPE Image to a temporary location
dism /Mount-Wim /WimFile:c:\build-winpe\razor-winpe\winpe.wim /index:1 /MountDir:C:\build-winpe\offline


##Adding standard modules to the WinPE image
cd \Program Files (x86)\Windows Kits\8.0\Assesment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\

dism /Image:C:\build-winpe\offline /Add-Package:WinPE-WMI.cab
dism /Image:C:\build-winpe\offline /Add-Package:WinPE-NetFX4.cab
dism /Image:C:\build-winpe\offline /Add-Package:WinPE-Scripting.cab
dism /Image:C:\build-winpe\offline /Add-Package:WinPE-PowerShell3.cab


##Create/Update the startup script

Open the file C:\build-winpe\offline\Windows\System32\startnet.cmd and replace the contents with the following:

	@echo off
	echo starting wpeinit to detect and boot network hardware
	wpeinit
	echo starting the razor client
	powershell -executionpolicy bypass -noninteractive -file %SYSTEMDRIVE%\razor-client.ps1
	echo dropping to a command shell now...

Save and close the file

##Install the Razor Powershell Script
You need to copy the razor-client.ps1 that is found in the /opt/razor/build-winpe directory on your razor server into C:\build-winpe\offline\Windows\System32\ folder

##Commit Changes and unmount the WinPE wim mount

	dism /Image:C:\build-winpe\offline /Commit-Wim
	dism /Image:C:\build-winpe\offline /Unmount-Wim


