# NetCoreMediatrSample
Sample and template for Mediatr pattern in .NET Core.

Some of the  dependencies are:
 - AutoFixture: For testing purpose.
 - Moq: For testing purpose by mocking dependencies.
 - AutoMapper: Eliminate a lot of boilerplate by auto mapping request or response.
 - FluentValidation: For validating requests before they are handled.
 - MediatR: For dispatching request/response, commands, queries, notifications and events.
 - FluentAssertions: Better and easier assertions in tests.
 - Hangfire: Background worker.
 - Entity Framework: Object-relatoinal mapping.
 - App.metrics: Real time metrics set up with InfluxDb and Grafana.
 - Microsoft Extensions Logging: Logging API.

 Running on .NET Core 2.1
 
 ## Structure
  - Src: Here goes the application.
  - DataModel: Here goes all the implementations for the database/store.
  - Test: Here goes all tests for the application.
 
 ### Src
 Src is structured by having a feature in a single file. That gives us the following structure:
  - Controllers: Here goes all the controllers without any logic.
  - Features: Here goes all the features (eg. User/GetUser.cs).
  - Infrastructure: Here goes the implementation for the application it self (eg. Middlewares, Filters, Pipeline).
  - ThirdParty: Here goes the implementation for third party services (eg. Facebook login).
  - Helpers: Shared services that can be used as helper function to different features.

## Setting up application
The appliaction requires 2 databases - one for the application and one for Hangfire.
 1. Create a new appsettings to your ASPNETCORE_ENVIRONMENT (eg appsettings.Development.json) and add the 2 new connection strings for application and Hangfire.
 2. Run database changes to the application database by running the command `dotnet ef database update -s ../Src` inside DataModel folder (see most of the commands in *DataModel/DatabaseContext.cs*).
 
## Setting up real time metrics
Real time metrics require Grafana and InfluxDb.
 1. Add InfluxDb options to appsettings.
 2. Download Grafana dashboard [here](https://grafana.com/dashboards/2125).

## Build and run with Docker
```
$ docker build -t aspnetapp .
$ docker run -d -p 8080:80 --name myapp aspnetapp
```
