﻿Start VS2019 in Admin mode:

 1. created with: dotnet new angular --auth Individual -uld
 2. added a custom V2 passwordhaser: services.Configure<PasswordHasherOptions>(option =>{option.CompatibilityMode = PasswordHasherCompatibilityMode.IdentityV2;});


TWO ERRORS, 1, scaffolding, 2. logout with IdentityServer endpoint "/.well-known/openid-configuration" failing


1. https://github.com/aspnet/AspNetCore/blob/master/src/Identity/UI/src/Areas/Identity/Pages/V4/Account/Login.cshtml#L53
has a pointless:
"See <a href="https://go.microsoft.com/fwlink/?LinkID=532715">this article</a> for details on setting up this ASP.NET application to support logging in via external services."

You have to scaffold the idenity login to remove it.

https://github.com/IdentityServer/IdentityServer4.Quickstart.UI/blob/master/Views/Account/Login.cshtml#L53
does not have it, so adopt that approach instead, or have a #DEBUG flag around it.


ERROR: in Adding Scaffolding with no layout, and an ApplicationUser DataContext, just for the account\login.cshtml page, the following error appears:

Finding the generator 'identity'...
Running the generator 'identity'...
There was an error running the template C:\Users\defaultuser\.nuget\packages\microsoft.visualstudio.web.codegenerators.mvc\3.0.0-preview5-19264-04\Templates\Identity\Pages\_Layout.cshtml: Template Processing Failed:(95,13): error CS0103: The name 'BeginWriteAttribute' does not exist in the current context
(96,13): error CS0103: The name 'EndWriteAttribute' does not exist in the current context
   at Microsoft.VisualStudio.Web.CodeGeneration.ActionInvoker.<BuildCommandLine>b__6_0()
   at Microsoft.Extensions.CommandLineUtils.CommandLineApplication.Execute(String[] args)
   at Microsoft.VisualStudio.Web.CodeGeneration.ActionInvoker.Execute(String[] args)
   at Microsoft.VisualStudio.Web.CodeGeneration.CodeGenCommand.Execute(String[] args)

Halfway through Scaffolding, message says "adding DI", then a Build kicked off with the VERBOSE log file: build.log.zip


2. Start, Login, Logout, IISExpress CRASH:
IdentityServer4.Hosting.IdentityServerMiddleware: Information: Invoking IdentityServer endpoint: IdentityServer4.Endpoints.DiscoveryEndpoint for /.well-known/openid-configuration
Microsoft.AspNetCore.Hosting.Diagnostics: Information: Request starting HTTP/2.0 GET https://localhost:44394/sockjs-node/info?t=1560740564510  
Microsoft.AspNetCore.Hosting.Diagnostics: Information: Request finished in 182.0859ms 200 application/json; charset=UTF-8
IdentityServer4.Endpoints.DiscoveryEndpoint: Debug: Start discovery request
Microsoft.AspNetCore.Hosting.Diagnostics: Information: Request finished in 225.4061ms 200 application/json; charset=UTF-8
Microsoft.AspNetCore.Hosting.Diagnostics: Information: Request finished in 306.63890000000004ms 0 
The program '[22672] iisexpress.exe' has exited with code -1 (0xffffffff).