# ChatGPT Note

Before starting the project:

1. Go to https://openai.com/api/
2. Log In
3. Click on "Personal"
4. Click on "View API Keys"
5. Click on "+ Create new secret key"
6. Keep your api key

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

After opening the VS Code, a message will be prompted on the right bottom. Click on "yes".

![Prompted message](https://github.com/tzubindev/chatgpt/blob/main/resource/prompted_message.png?raw=true)

### Add Packages

To open terminal, press `CTRL + ~`

Then

    dotnet add package Newtonsoft.Json

The csproj file should be updated:

![Add package](https://github.com/tzubindev/chatgpt/blob/main/resource/add_package_newtonsoftjson.png?raw=true)

Also adding TextCopy package

    dotnet add package TextCopy

### Code in Program.cs

Code these in the file:

    using System.Text;

    if (args.Length > 0) // here to receive arguments
    {
        // Create request obj
        HttpClient client = new HttpClient();

        // Add Header
        client.DefaultRequestHeaders.Add("authorization", "Bearer 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");

        // Create content
        var content = new StringContent("{\"model\": \"text-davinci-001\", \"prompt\": \"" + args[0] + "\",\"temperature\": 1, \"max_tokens\": 100}",
            Encoding.UTF8, "application/json");

        // Get response through endpoint by passing content
        HttpResponseMessage response = await client.PostAsync("https://api.openai.com/v1/completions", content);

        // Wait for response
        string responseString = await response.Content.ReadAsStringAsync();

        Console.WriteLine(responseString);
    }
    else
    {
        Console.WriteLine("---> You need to provide some input.");
    }

Save the file and run these commands:

    dotnet build

    dotnet run --"WRITE YOUR QUESTION HERE."

A JSON object will be returned.

After that, update the code

    using System.Text;
    using Newtonsoft.Json;

    if (args.Length > 0) // here to receive arguments
    {
        // Create request obj
        HttpClient client = new HttpClient();

        // Add Header
        client.DefaultRequestHeaders.Add("authorization", "Bearer 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");

        // Create content
        var content = new StringContent("{\"model\": \"text-davinci-003\", \"prompt\": \"" + args[0] + "\",\"temperature\": 1, \"max_tokens\": 100}",
            Encoding.UTF8, "application/json");

        // Get response through endpoint by passing content
        HttpResponseMessage response = await client.PostAsync("https://api.openai.com/v1/completions", content);

        // Wait for response
        string responseString = await response.Content.ReadAsStringAsync();

        try
        {
            // Deserialise Data
            var dyData = JsonConvert.DeserializeObject<dynamic>(responseString);

            Console.ForegroundColor = ConsoleColor.Green;
            Console.WriteLine($"---> API response is: {dyData!.choices[0].text}");
            Console.ResetColor();
        }
        catch (Exception ex)
        {
            Console.WriteLine($"---> Could not deserialise the JSON: {ex.Message}");
        }
    }
    else
    {
        Console.WriteLine("---> You need to provide some input.");
    }

Update property group in csproj:

  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>net7.0</TargetFramework>
    <ImplicitUsings>enable</ImplicitUsings>
    <Nullable>enable</Nullable>
    <PublishSingleFile>true</PublishSingleFile>
    <SelfContained>true</SelfContained>
    <RuntimeIdentifier>win-x64</RuntimeIdentifier>
    <PlubishReadyToRun>true</PlubishReadyToRun>
    <DebugType>embedded</DebugType>
  </PropertyGroup>

Then run this code to publish app to the current repo: (for window user)

    dotnet publish -r win-x64
