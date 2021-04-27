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

4. Add connection strings:



```
  "ConnectionStrings": {
    "ConfigurationDbConnection": "Server=xxxxxx;Database=IdentityServerConfigurationDb;User ID=xxxxxx;password=xxxxxx;Trusted_Connection=True;MultipleActiveResultSets=true",
    "PersistedGrantDbConnection": "Server=xxxxxx;Database=IdentityServerPersistedGrantDb;User ID=xxxxxx;password=xxxxxx;Trusted_Connection=True;MultipleActiveResultSets=true",
    "IdentityDbConnection": "Server=xxxxxx;Database=AdminIdentityDb;User ID=xxxxxx;password=xxxxxx;Trusted_Connection=True;MultipleActiveResultSets=true",
    "AdminLogDbConnection": "Server=xxxxxx;Database=AdminLogDb;User ID=xxxxxx;password=xxxxxx;Trusted_Connection=True;MultipleActiveResultSets=true",
    "AdminAuditLogDbConnection": "Server=xxxxxx;Database=AdminAuditLogDb;User ID=xxxxxx;password=xxxxxx;Trusted_Connection=True;MultipleActiveResultSets=true",
    "DataProtectionDbConnection": "Server=xxxxxx;Database=IdentityServerDataProtectionDb;User ID=xxxxxx;password=xxxxxx;Trusted_Connection=True;MultipleActiveResultSets=true"
  },


```

5. Run seed for migration and admin user:

```
dotnet run /seed

```
