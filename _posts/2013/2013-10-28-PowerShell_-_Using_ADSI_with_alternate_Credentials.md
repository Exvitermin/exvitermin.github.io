---
layout: single
title: PowerShell - Using ADSI with alternate Credentials
excerpt: 
permalink: /2013/10/powershell-using-adsi-with-alternate.html
tags: 
- active directory
- adsi
- credentials
- function
- powershell
published: true
comments: true
---
<a href="{{ site.url }}/images/2013/20131028_PowerShell_-_Using_ADSI_with_alternate_Credentials/022__2014673127__-128x128.png" imageanchor="1" style="clear: left; float: left; margin-bottom: 1em; margin-right: 1em;"><img border="0" src="{{ site.url }}/images/2013/20131028_PowerShell_-_Using_ADSI_with_alternate_Credentials/022__2014673127__-128x128.png" /></a>The following PowerShell code will show you how to run ADSI with alternate credentials to get information from the Active Directory.

I will query Group objects in this example, my filter is define by the following line:"(objectCategory=Group)"






### Using ADSI with alternate Credentials


```
#Define the Credential
$Credential = Get-Credential -Credential FX\catfx

# Create an ADSI Search    
$Searcher = New-Object -TypeName System.DirectoryServices.DirectorySearcher

# Get only the Group objects
$Searcher.Filter = "(objectCategory=Group)"

# Limit the output to 50 objects
$Searcher.SizeLimit = '50'

# Get the current domain
$DomainDN = $(([adsisearcher]"").Searchroot.path)

# Create an object "DirectoryEntry" and specify the domain, username and password
$Domain = New-Object -TypeName System.DirectoryServices.DirectoryEntry -ArgumentList $DomainDN ,$($Credential.UserName),$($Credential.GetNetworkCredential().password)

# Add the Domain to the search
$Searcher.SearchRoot = $Domain

# Execute the Search
$Searcher.FindAll()
```



### Output



```
PS C:\> $Searcher.FindAll()

Path                                              Properties
----                                              ----------
LDAP://CN=WinRMRemoteWMIUsers__,CN=Users,DC=FX... {usnchanged, distinguishedname, grouptype, whe...
LDAP://CN=Administrators,CN=Builtin,DC=FX,DC=LAB  {objectcategory, usnchanged, distinguishedname...
LDAP://CN=Users,CN=Builtin,DC=FX,DC=LAB           {usnchanged, distinguishedname, grouptype, whe...
LDAP://CN=Guests,CN=Builtin,DC=FX,DC=LAB          {usnchanged, distinguishedname, grouptype, whe...
LDAP://CN=Print Operators,CN=Builtin,DC=FX,DC=LAB {iscriticalsystemobject, usnchanged, distingui...
LDAP://CN=Backup Operators,CN=Builtin,DC=FX,DC... {iscriticalsystemobject, usnchanged, distingui...
LDAP://CN=Replicator,CN=Builtin,DC=FX,DC=LAB      {iscriticalsystemobject, usnchanged, distingui...
LDAP://CN=Remote Desktop Users,CN=Builtin,DC=F... {iscriticalsystemobject, usnchanged, distingui...
LDAP://CN=Network Configuration Operators,CN=B... {iscriticalsystemobject, usnchanged, distingui...
LDAP://CN=Performance Monitor Users,CN=Builtin... {iscriticalsystemobject, usnchanged, distingui...
LDAP://CN=Performance Log Users,CN=Builtin,DC=... {iscriticalsystemobject, usnchanged, distingui...
LDAP://CN=Distributed COM Users,CN=Builtin,DC=... {iscriticalsystemobject, usnchanged, distingui...
LDAP://CN=IIS_IUSRS,CN=Builtin,DC=FX,DC=LAB       {usnchanged, distinguishedname, grouptype, whe...
LDAP://CN=Cryptographic Operators,CN=Builtin,D... {iscriticalsystemobject, usnchanged, distingui...
LDAP://CN=Event Log Readers,CN=Builtin,DC=FX,D... {iscriticalsystemobject, usnchanged, distingui...
LDAP://CN=Certificate Service DCOM Access,CN=B... {iscriticalsystemobject, usnchanged, distingui...
LDAP://CN=RDS Remote Access Servers,CN=Builtin... {iscriticalsystemobject, usnchanged, distingui...
LDAP://CN=RDS Endpoint Servers,CN=Builtin,DC=F... {iscriticalsystemobject, usnchanged, distingui...
LDAP://CN=RDS Management Servers,CN=Builtin,DC... {iscriticalsystemobject, usnchanged, distingui...
LDAP://CN=Hyper-V Administrators,CN=Builtin,DC... {iscriticalsystemobject, usnchanged, distingui...
LDAP://CN=Access Control Assistance Operators,... {iscriticalsystemobject, usnchanged, distingui...
LDAP://CN=Remote Management Users,CN=Builtin,D... {iscriticalsystemobject, usnchanged, distingui...
LDAP://CN=Domain Computers,CN=Users,DC=FX,DC=LAB  {iscriticalsystemobject, usnchanged, distingui...
LDAP://CN=Domain Controllers,CN=Users,DC=FX,DC... {usnchanged, distinguishedname, grouptype, whe...
LDAP://CN=Schema Admins,CN=Users,DC=FX,DC=LAB     {objectcategory, usnchanged, distinguishedname...
LDAP://CN=Enterprise Admins,CN=Users,DC=FX,DC=LAB {objectcategory, usnchanged, distinguishedname...
LDAP://CN=Cert Publishers,CN=Users,DC=FX,DC=LAB   {usnchanged, distinguishedname, grouptype, whe...
LDAP://CN=Domain Admins,CN=Users,DC=FX,DC=LAB     {objectcategory, usnchanged, distinguishedname...
LDAP://CN=Domain Users,CN=Users,DC=FX,DC=LAB      {usnchanged, distinguishedname, grouptype, whe...
LDAP://CN=Domain Guests,CN=Users,DC=FX,DC=LAB     {usnchanged, distinguishedname, grouptype, whe...
LDAP://CN=Group Policy Creator Owners,CN=Users... {usnchanged, distinguishedname, grouptype, whe...
LDAP://CN=RAS and IAS Servers,CN=Users,DC=FX,D... {iscriticalsystemobject, usnchanged, distingui...
LDAP://CN=Server Operators,CN=Builtin,DC=FX,DC... {iscriticalsystemobject, usnchanged, distingui...
LDAP://CN=Account Operators,CN=Builtin,DC=FX,D... {iscriticalsystemobject, usnchanged, distingui...
LDAP://CN=Pre-Windows 2000 Compatible Access,C... {usnchanged, distinguishedname, grouptype, whe...
LDAP://CN=Incoming Forest Trust Builders,CN=Bu... {iscriticalsystemobject, usnchanged, distingui...
LDAP://CN=Windows Authorization Access Group,C... {usnchanged, distinguishedname, grouptype, whe...
LDAP://CN=Terminal Server License Servers,CN=B... {iscriticalsystemobject, usnchanged, distingui...
LDAP://CN=Allowed RODC Password Replication Gr... {iscriticalsystemobject, usnchanged, distingui...
LDAP://CN=Denied RODC Password Replication Gro... {usnchanged, distinguishedname, grouptype, whe...
LDAP://CN=Read-only Domain Controllers,CN=User... {usnchanged, distinguishedname, grouptype, whe...
LDAP://CN=Enterprise Read-only Domain Controll... {iscriticalsystemobject, usnchanged, distingui...
LDAP://CN=Cloneable Domain Controllers,CN=User... {iscriticalsystemobject, usnchanged, distingui...
LDAP://CN=DnsAdmins,CN=Users,DC=FX,DC=LAB         {usnchanged, distinguishedname, grouptype, whe...
LDAP://CN=DnsUpdateProxy,CN=Users,DC=FX,DC=LAB    {usnchanged, distinguishedname, grouptype, whe...
LDAP://CN=esx admins,OU=Local,OU=Administratio... {usnchanged, distinguishedname, grouptype, whe...
LDAP://CN=ScorchUsers,OU=Global,OU=Administrat... {usnchanged, distinguishedname, grouptype, whe...
LDAP://CN=Test Jonathan Group,CN=Users,DC=FX,D... {usnchanged, distinguishedname, grouptype, whe...

```




### Credentials

The key here to pass the credentials is the .NET Class <a href="http://msdn.microsoft.com/en-us/library/system.directoryservices.directoryentry.aspx" target="_blank">System.DirectoryServices.DirectoryEntry</a>
<a href="http://3.bp.blogspot.com/-g669rSYWxKI/Um8tITxbFvI/AAAAAAABeXM/2ax-024y2aI/s1600/2013-10-28+11-33-37+PM.png" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img border="0" height="521" src="http://3.bp.blogspot.com/-g669rSYWxKI/Um8tITxbFvI/AAAAAAABeXM/2ax-024y2aI/s640/2013-10-28+11-33-37+PM.png" width="640" /></a>


If you inspect each of the constructors below, you will notice one accept a path, a username and a password <span style="font-family: Courier New, Courier, monospace;">DirectoryEntry(String,String,String)
<a href="http://2.bp.blogspot.com/-tKLMwoOd8DQ/Um8uZwUJdII/AAAAAAABeXY/TnieNshPRUE/s1600/2013-10-28+11-36-51+PM.png" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img border="0" src="http://2.bp.blogspot.com/-tKLMwoOd8DQ/Um8uZwUJdII/AAAAAAABeXY/TnieNshPRUE/s1600/2013-10-28+11-36-51+PM.png" /></a>

Which mean : <span style="font-family: Courier New, Courier, monospace;">DirectoryEntry(path,username,password)
<a href="http://1.bp.blogspot.com/-omDSMlPAeSo/Um8urb6ILdI/AAAAAAABeXo/4rWPprYV_ZI/s1600/2013-10-28+11-37-59+PM.png" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img border="0" src="http://1.bp.blogspot.com/-omDSMlPAeSo/Um8urb6ILdI/AAAAAAABeXo/4rWPprYV_ZI/s1600/2013-10-28+11-37-59+PM.png" /></a>
That's exactly what I used in the following line
```
New-Object -TypeName System.DirectoryServices.DirectoryEntry -ArgumentList $DomainDN ,$($Credential.UserName),$($Credential.GetNetworkCredential().password)
```

<b><span style="font-family: Courier New, Courier, monospace;">$DomainDN</b>contains the path of current domain : "LDAP://DC=FX,DC=LAB"
<b><span style="font-family: Courier New, Courier, monospace;">$($Credential.UserName)</b>contains the username specify : "FX\Catfx"
<b><span style="font-family: Courier New, Courier, monospace;">$($Credential.GetNetworkCredential().password)</b>contains the password



### More Properties

Additionally if you want to get other properties, you will need to dig a bit


```
PS C:\> ($Searcher.FindAll())[0].properties

Name                           Value
----                           -----
usnchanged                     {8198}
distinguishedname              {CN=WinRMRemoteWMIUsers__,CN=Users,DC=FX,DC=LAB}
grouptype                      {-2147483644}
whencreated                    {3/7/2013 2:17:57 AM}
samaccountname                 {WinRMRemoteWMIUsers__}
objectsid                      {1 5 0 0 0 0 0 5 21 0 0 0 180 190 60 92 74 161 105 103 20 195 233...
instancetype                   {4}
adspath                        {LDAP://CN=WinRMRemoteWMIUsers__,CN=Users,DC=FX,DC=LAB}
usncreated                     {8198}
whenchanged                    {3/7/2013 2:17:57 AM}
cn                             {WinRMRemoteWMIUsers__}
samaccounttype                 {536870912}
objectguid                     {140 74 31 5 221 174 220 65 177 222 155 20 54 101 97 89}
objectcategory                 {CN=Group,CN=Schema,CN=Configuration,DC=FX,DC=LAB}
description                    {Members of this group can access WMI resources over management p...
objectclass                    {top, group}
dscorepropagationdata          {3/7/2013 2:19:52 AM, 1/1/1601 12:00:01 AM}
name                           {WinRMRemoteWMIUsers__}
```



