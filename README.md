# ChatGPT Note

## Check dotnet version

Version 6.0 and above would be fine.

    dotnet --version

## Create template Console App "ask"

    dotnet new console -n ask

The following output:

    Welcome to .NET 7.0!
    ---------------------
    SDK Version: 7.0.101

    Telemetry
    ---------
    The .NET tools collect usage data in order to help us improve your experience. It is collected by Microsoft and shared with the community. You can opt-out of telemetry by setting the DOTNET_CLI_TELEMETRY_OPTOUT environment variable to '1' or 'true' using your favorite shell.

    Read more about .NET CLI Tools telemetry: https://aka.ms/dotnet-cli-telemetry

    ----------------
    Installed an ASP.NET Core HTTPS development certificate.
    To trust the certificate run 'dotnet dev-certs https --trust' (Windows and macOS only).
    Learn about HTTPS: https://aka.ms/dotnet-https
    ----------------
    Write your first app: https://aka.ms/dotnet-hello-world
    Find out what's new: https://aka.ms/dotnet-whats-new
    Explore documentation: https://aka.ms/dotnet-docs
    Report issues and find source on GitHub: https://github.com/dotnet/core
    Use 'dotnet --help' to see available commands or visit: https://aka.ms/dotnet-cli
    --------------------------------------------------------------------------------------
    The template "Console App" was created successfully.

    Processing post-creation actions...
    Restoring C:\Users\devtb\S7E1\ask\ask.csproj:
    Determining projects to restore...
    Restored C:\Users\devtb\S7E1\ask\ask.csproj (in 58 ms).
    Restore succeeded.

## Check what's in the repo

To move to the repo:

    cd ask

To list all items:

    ls

The following output:

    Mode                 LastWriteTime         Length Name
    ----                 -------------         ------ ----
    d-----        02/02/2023     09:27                obj
    -a----        02/02/2023     09:27            249 ask.csproj
    -a----        02/02/2023     09:27            105 Program.cs

Open in VS Code:

    code .

## Code in VS Code

After opening the VS Code, a message will be prompted on the right bottom.

![Prompted message](https://github.com/tzubindev/chatgpt/blob/main/resource/prompted_message.png?raw=true)
