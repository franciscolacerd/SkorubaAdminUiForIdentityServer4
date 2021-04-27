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

4. Add connection strings in appsettings.json:



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

5. Add log connection string at serilog.json:


```
            {
                "Name": "MSSqlServer",
              "Args": {
                "connectionString": "Server=xxxxxx;Database=AdminLogDb;User ID=xxxxxx;password=xxxxxx;Trusted_Connection=True;MultipleActiveResultSets=true",
                "tableName": "Log",
                "columnOptionsSection": {
                  "addStandardColumns": [ "LogEvent" ],
                  "removeStandardColumns": [ "Properties" ]
                }
              }
            }

```

6. Change identityserverdata.json information :

```
{
    "IdentityServerData": {
        "IdentityResources": [
            {
                "Name": "roles",
                "Enabled": true,
                "DisplayName": "Roles",
                "UserClaims": [
                    "role"
                ]
            },
            {
                "Name": "openid",
                "Enabled": true,
                "Required": true,
                "DisplayName": "Your user identifier",
                "UserClaims": [
                    "sub"
                ]
            },
            {
                "Name": "profile",
                "Enabled": true,
                "DisplayName": "User profile",
                "Description": "Your user profile information (first name, last name, etc.)",
                "Emphasize": true,
                "UserClaims": [
                    "name",
                    "family_name",
                    "given_name",
                    "middle_name",
                    "nickname",
                    "preferred_username",
                    "profile",
                    "picture",
                    "website",
                    "gender",
                    "birthdate",
                    "zoneinfo",
                    "locale",
                    "updated_at"
                ]
            },
            {
                "Name": "email",
                "Enabled": true,
                "DisplayName": "Your email address",
                "Emphasize": true,
                "UserClaims": [
                    "email",
                    "email_verified"
                ]
            },
            {
                "Name": "address",
                "Enabled": true,
                "DisplayName": "Your address",
                "Emphasize": true,
                "UserClaims": [
                    "address"
                ]
            }
        ],
        "ApiScopes": [
            {
                "Name": "flacerda_api",
                "DisplayName": "flacerda_api",
                "Required": true,
                "UserClaims": [
                    "role",
                    "name"
                ]
            }
        ],
        "ApiResources": [
            {
                "Name": "flacerda_api",
                "Scopes": [
                    "flacerda_api"
                ]
            }
        ],
        "Clients": [
            {
                "ClientId": "flacerda",
                "ClientName": "flacerda",
                "ClientUri": "https://localhost:44303",
                "AllowedGrantTypes": [
                    "authorization_code"
                ],
                "RequirePkce": true,
                "ClientSecrets": [
                    {
                        "Value": "3ba57ce1-6a5d-4ca6-aa95-2aacb68ebe13"
                    }
                ],
                "RedirectUris": [
                    "https://localhost:44303/signin-oidc"
                ],
                "FrontChannelLogoutUri": "https://localhost:44303/signout-oidc",
                "PostLogoutRedirectUris": [
                    "https://localhost:44303/signout-callback-oidc"
                ],
                "AllowedCorsOrigins": [
                    "https://localhost:44303"
                ],
                "AllowedScopes": [
                    "openid",
                    "email",
                    "profile",
                    "roles"
                ]
            },
            {
                "ClientId": "flacerda_api_swaggerui",
                "ClientName": "flacerda_api_swaggerui",
                "AllowedGrantTypes": [
                    "authorization_code"
                ],
                "RequireClientSecret": false,
                "RequirePkce": true,
                "RedirectUris": [
                    "https://localhost:44302/swagger/oauth2-redirect.html"
                ],
                "AllowedScopes": [
                    "flacerda_api"
                ],
                "AllowedCorsOrigins": [
                    "https://localhost:44302"
                ]
            }
        ]
    }
}
```

7. Right mouse on solution and choose Multiple Startup Projects:

![image](https://user-images.githubusercontent.com/6674269/116260594-b92e6a00-a76e-11eb-876d-e67aae7ddbe5.png)


8. Run seed for migration and admin user:

```
dotnet run /seed

```
