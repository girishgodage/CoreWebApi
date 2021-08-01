# CoreWebApi

An Implementation of Clean Architecture with ASP.NET Core 3.1 WebApi. With this Open-Source BoilerPlate Template, you will get access to the world of Loosely-Coupled and Inverted-Dependency Architecture in ASP.NET Core 3.1 WebApi with a lot of best practices.

## Releases
v1.0 -  Release - [Download the Release](https://github.com/girishgodage/CoreWebApi/releases/tag/v1) 


## Getting Started

Follow these steps to get started with this Boiler Plate Template.

### Download the Extension
Make sure Visual Studio 2019 is installed on your machine with the latest SDK.
[Download from Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=GirishGodage.CoreWebApi). Install it on your machine.

1. Open up Visual Studio 2019 and Click on Create New Project
1. Search for CoreWebApi. You can find the newly installed Project Template. Click on it and Press Create.
1. Once Visual Studio is done creating your new Project, Navigate to appsettings.json and change the Connection String to your preferred one.
1. Here you can choose to have multiple DBs for a separation of the IdentityDB or have the same DB for Identity and Application.
1. Once that is Set, Run these commands to update the database.
 
- update-database -Context IdentityContext

- update-database -Context ApplicationDbContext

1. Finally, build and run the Application.

### Alternatively you can also clone the Repository.

1. Clone this Repository and Extract it to a Folder.
3. Change the Connection Strings for the Application and Identity in the WebApi/appsettings.json - (WebApi Project)
2. Run the following commands on Powershell in the WebApi Projecct's Directory.
- dotnet restore
- dotnet ef database update -Context ApplicationDbContext
- dotnet ef database update -Context IdentityContext
- dotnet run (OR) Run the Solution using Visual Studio 2019

### How to use MySQL or PostgreSQL as your Data Provider
The Project currently uses MSSQL as the default Data Provider. If you are more comfortable with MySQL or PostgreSQL, here is how to migrate to them easily.


1. delete all existing file inside migrations folder on both project
   - Infrastructure.Identity
   - Infrastructure.Persistence

2. In in `ServiceExtensions.cs` and `ServiceRegistration.cs` change from `options.UseSqlServer` to:
#### For MySql
`options.UseMySql`
#### For PostgreSQL
`options.UseNpgsql`

3. Add NuGet packages to both projects (Infrastructure.Identity and Infrastructure.Persistence):
#### For MySql:
run `dotnet add package Pomelo.EntityFrameworkCore.MySql --version 3.1.2` (remember to do this on both projects)
#### For PostgreSQL:
run 
```cli
dotnet add package Npgsql.EntityFrameworkCore.PostgreSQL
dotnet add package Npgsql.EntityFrameworkCore.PostgreSQL.Design
```
(remember to do this on both projects)

4. on `IdentityContext.cs` comment `builder.HasDefaultSchema("Identity");` because ef doesn't support that on mysql

5. cd to `Infrastructure.Identity` and run
   - `dotnet ef database update --startup-project ../{YourProjectName}/{YourProjectName}.csproj -c "IdentityContext"`
   - `dotnet ef migrations add Initial --startup-project ../{YourProjectName}/{YourProjectName}.csproj -c "IdentityContext"`

6. cd to `Infrastructure.Persistence` and run
   - `dotnet ef database update --startup-project ../{YourProjectName}/{YourProjectName}.csproj -c "ApplicationDbContext"`
   - `dotnet ef migrations add Initial --startup-project ../{YourProjectName}/{YourProjectName}.csproj -c "ApplicationDbContext"`
   
The above guide (To use MySQL) was contributed by [geekz-reno](https://github.com/geekz-reno).

### Default Roles & Credentials
As soon you build and run your application, default users and roles get added to the database.

Default Roles are as follows.
- SuperAdmin
- Admin
- Moderator
- Basic

Here are the credentials for the default users.
- Email - superadmin@gmail.com  / Password - 123Pa$$word!
- Email - basic@gmail.com  / Password - 123Pa$$word!

You can use these default credentials to generate valid JWTokens at the ../api/account/authenticate endpoint.

## Purpose of this Project

Does it really make sense to Setup your ASP.NET Core Solution everytime you start a new WebApi Project ? Aren't we wasting quite a lot of time in doing this over and over gain?

This is the exact Problem that I intend to solve with this Full-Fledged ASP.NET Core 3.1 WebApi Solution Template, that also follows various principles of Clean Architecture.

The primary goal is to create a Full-Fledged implementation, that is well documented along with the steps taken to build this Solution from Scratch. This Solution Template will also be available within Visual Studio 2019 (by installing the required Nuget Package / Extension).
- Demonstrate Clean Monolith Architecture in ASP.NET Core 3.1 
- This is not a Proof of Concept
- Implementation that is ready for Production
- Integrate the most essential libraries and packages

## Give a Star ⭐️
If you found this Implementation helpful or used it in your Projects, do give it a star. Thanks!

## Technologies
- ASP.NET Core 3.1 WebApi
- REST Standards
- .NET Core 3.1 / Standard 2.1 Libraries

## Features
- [x] Onion Architecture
- [x] CQRS with MediatR Library
- [x] Entity Framework Core - Code First
- [x] Repository Pattern - Generic
- [x] MediatR Pipeline Logging & Validation
- [x] Serilog
- [x] Swagger UI
- [x] Response Wrappers
- [x] Healthchecks
- [x] Pagination
- [ ] In-Memory Caching
- [ ] Redis Caching
- [x] In-Memory Database
- [x] Microsoft Identity with JWT Authentication
- [x] Role based Authorization
- [x] Identity Seeding
- [x] Database Seeding
- [x] Custom Exception Handling Middlewares
- [x] API Versioning
- [x] Fluent Validation
- [x] Automapper
- [x] SMTP / Mailkit / Sendgrid Email Service
- [x] Complete User Management Module (Register / Generate Token / Forgot Password / Confirmation Mail)
- [x] User Auditing
