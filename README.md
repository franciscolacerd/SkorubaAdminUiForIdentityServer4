# SkorubaAdminUiForIdentityServer4

TOOLS - How to create a Skoruba Admin Ui for IdentityServer4


https://github.com/skoruba/IdentityServer4.Admin



1. Install template:


```
dotnet new -i Skoruba.IdentityServer4.Admin.Templates::2.0.1
```

2. Create project:

```
dotnet new skoruba.is4admin --name MyProject --title MyProject --adminemail "admin@example.com" --adminpassword "Pa$$word123" --adminrole MyRole --adminclientid MyClientId --adminclientsecret MyClientSecret --dockersupport true

```

3. Create 6 database for app suport and identity server suport:


AdminIdentityDb
IdentityServerConfigurationDb
IdentityServerPersistedGrantDb
AdminLogDb
AdminAuditLogDb
IdentityServerDataProtectionDb



![image](https://user-images.githubusercontent.com/6674269/116256020-b598e400-a76a-11eb-8d66-7798441fc79f.png)

