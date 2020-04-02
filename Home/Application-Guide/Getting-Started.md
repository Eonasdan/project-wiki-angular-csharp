# Requirements
[.NET Core 2.2](https://dotnet.microsoft.com) 

[NodeJS & NPM](https://nodejs.org/en/)

# Build and Run
1. Clone the repo <br/>
`git clone REPLACE ME`

1. Compile and build the projects as well as client app. <br/>
   1. cd into cloned repo `cd A02`
   2. run the build file `.\build.cmd`

## Visual Studio
1. Open the solution file
1. Edit the User Secrets by right click on the web project and clicking "Manage User Secrets".
    > *Note:* the value for server within the connection string can vary depending on how you have SQL configured.
    ```
    {
        "ConnectionStrings": {
            "DefaultConnection": "Server=localhost;Database=REPLACEME;Trusted_Connection=True"
        }
    }
    ```

1. Run migrations to initialize the database
   1. Open the package manager console.
   1. Select the data access layer (DAL).
   1. Run migrations using `Update-Database`. Please make sure that you have DAL selected as the default project within the package manager console before executing the above command.<br/>

1. Set the default project within VS to the web project (right click -> Set as Startup Project)

## Visual Studio Code
1. Within the directory that you just cloned, open the project in VS Code by running `code .`

1.  Bring up the integrated terminal by pressing Ctrl+` and set your user secrets
    > *Note:* the value for server within the connection string can vary depending on how you have SQL configured. <br/>

    `dotnet user-secrets set "ConnectionStrings:DefaultConnection" "Server=localhost;Database=REPLACEME;Trusted_Connection=True"`

5. Run migrations
   1. `cd INTO DAL Folder`
   1. `dotnet ef datbase update`

6. Run the app
   1. `cd INTO Web Folder`
   1. `dotnet run`