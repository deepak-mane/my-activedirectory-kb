# my-activedirectory-kb
Learn tips and tricks related to accessing and using active directory

## Blogs/Articles
1. [Powershell-arrays-Everything-you-wanted-to-know](https://powershellexplained.com/2018-10-15-Powershell-arrays-Everything-you-wanted-to-know/)


### Search Active Directory Groups with Wildcard
To work around this problem, my recommendation is to use the PowerShell ActiveDirectory module. See the following for some hints on how to use:
```
Open the PowerShell command window
Get-Module -ListAvailable
Import-Module ActiveDirectory
Get-ADGroup -Filter {name -like "*aid*"} -Properties Description,info | Select Name,samaccountname,Description,info | Sort Name
Get-ADGroupMember YourGroupName # to list members
Using a “-like” filter against the “name” property allows the standard wildcard match (*/star/asterisk/glob) which will match any sequence of characters within the group name.
This example would match group names like: Aids-Research, Hearing-Aids, Raiders, etc.
```

ADUC is missing this type of AD wildcard group search, but at least this is a simple way to do the search with Microsoft standard tools ;-). 
ADUC does the standard starts-with type of search, so it works for groups where you know the starting characters to search for. 
See comments of this post for a hint on using ADUC “Custom Search” Advanced search for patterns like name=*something* (ldap query syntax used for advanced custom search).


### To get all properties of User
```
Get-ADUser <USERID> -Properties *
```

### To Gret Group details
```
get-adgroup -Filter 'GroupCategory -eq "Security" -and GroupScope -ne "DomainLocal"'
get-adgroup -Filter 'Name -eq "AB_Roles_Approvers"'
get-adgroup -Identity "CN=AB_Roles_Approvers,OU=Access,OU=PINGPONG Prod,OU=PINGPONG Groups,OU=Application Groups,OU=Groups,..."
Get-ADGroup -Filter {name -like "SN_*"} -Properties Description,info | Select Name,samaccountname,Description,info | Sort Name

```
