# Contributing to BlazorWebFormsComponents

Thank you for taking the time to consider contributing to our project.

The following is a set of guidelines for contributing to the project.  These are mostly guidelines, not rules, and can be changed in the future.  Please submit your suggestions with a pull-request to this document.

1. [Code of Conduct](#code-of-conduct)
1. [What should I know before I get started?](#what-should-i-know-before-i-get-started?)
    1. [Project Folder Structure](#project-folder-structure)
    1. [Design Decisions](#design-decisions)
1. [How can I contribute?](#how-can-i-contribute?)
    1. [Tell us your story](#tell-us-your-story)
    1. [Write code for a component](#write-code-for-a-component)
    1. [Write documentation](#write-documentation)


## Code of Conduct

We have adopted a code of conduct from the Contributor Covenant.  Contributors to this project are expected to adhere to this code.  Please report unwanted behavior to [jeff@jeffreyfritz.com](mailto:jeff@jeffreyfritz.com)

## What should I know before I get started?

This project is currently a single library that will provide a shim, a buffer that will help you convert markup to run in Blazor. The project will grow in the future to support more automated conversion from ASP<span></span>.NET Web Forms to Blazor.

### Project Folder Structure

This project is designed to be built and run primarily with Visual Studio 2019. The folders are configured so that they will support editing and working in other editors and on non-Windows operating systems.  We encourage you to develop with these other environments, because we would like to be able to support developers who use those tools as well.  The folders are configured as follows:

```
/docs                                 -- User Documentation
/samples                              -- Usage Samples
  BeforeWebForms
  AfterBlazorClientSide               -- Shell project with WebAssembly config
  AfterBlazorServerSide               -- Shared project with Server-Side config
    /Pages/ControlSamples/COMPONENT_NAME/SCENARIO.razor
/src                                  -- Library source and unit tests
  BlazorWebFormsComponents
  BlazorWebFormsComponents.Test
    /COMPONENT_NAME/test.razor        -- Unit tests
```



We may add a top level `tests` folder if there are integration tests to show at some point.

All official versions of the project are built and delivered with Azure DevOps Pipelines and linked in the main README.md and [releases tab in GitHub](https://github.com/FritzAndFriends/BlazorWebFormsComponents/releases).

### Design Decisions

Design for this project is ultimately decided by the project lead, [Jeff Fritz](https://github.com/csharpfritz).  The following project tenets are adhered to when making decisions:

1. All attributes of the original controls should be supported. This helps emphasize the 'convert your markup' feature.
1. HTML markup generated by the components should replicate the markup generated by the original controls.  This helps to ensure the components behave as the Web Forms controls were expected to.
1. Minimal .NET APIs should be supported, in order to present the API.  The following are the primary APIs available:
    1. Component events: OnInit, OnLoad, OnPrerender, OnUnload
    1. DataBind()
1. The following APIs and Controls will NOT be supported:
    1. **DataSources** - These are components that provide connectivity to a data source.  In Blazor, this code should be moved to a Repository pattern and classes.  You can still connect that Repository to the components and work with the data.
    1. **ViewState** - There is no viewstate in Blazor.  ViewState is marked obsolete on components, and state of your interactions with the controls should be stored in private variables or Session.
    1. **Postback** - There is no postback in Blazor, therefore we will not support this feature.

## How can I contribute?

We are always looking for help on this project.  There are many millions of applications built that target ASP<span></span>.NET Web Forms, and we need your help building and identifying scenarios that need to be supported.  There are several ways that you can help:

### Tell us your story

Tell us how you are currently using the web forms framework so that we can build to meet your needs.  This means one of several types of contributions:

1. Send a pull request with a sample page that shows your scenario in the `samples/BeforeWebForms` project
1. Send a pull request with your desired scenario as a unit test in `src/BlazorWebFormsComponents.Test`
1. [Report an issue](https://github.com/FritzAndFriends/BlazorWebFormsComponents/Issues) with the details of a bug that you have found.  Be sure to tag it as a `Bug` so that we can triage and track it

### Write some Web Forms sample code

Demonstrate how an existing control is being used in the `BeforeWebForms` project.  The content of this sample project will be compiled and uploaded to the https://beforewebforms.azurewebsites.net location.

### Write code for a component

All code for a component should have an assigned issue that matches it.  This way we can prevent contributors from working on the same feature at the same time.

Any code that is written to support a component are required to be accompanied with unit tests at the time the pull request is submitted.  Pull requests without unit tests will be delayed and asked for unit tests to prove their functionality.  We use the [bUnit](https://www.nuget.org/packages/bunit/) to test our components.

Code for components' features should also include some definition in the `/docs` folder so that our users can identify and understand which feature is supported.

### Write documentation

The documentation for the migration and consumption of these components will be significant in scope and need to cover many scenarios.  We are always looking for help to add content to the `/docs` section of the repository with proper links back through to the main `/README.md`.
