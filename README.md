<img src="https://github.com/hypar-io/sdk/blob/master/hypar_logo.svg" width="200px" style="display: block;margin-left: auto;margin-right: auto;width: 50%;">

# generator
This is a generator. A generator is a function which receives a `Model`, does some compute, and returns a `Model`. Generators can take additional `inputs`, and output additional `outputs` as well.

By managing your generator as code, you can take advantage of all the great tools for code collaboration and deployment offered by GitHub. Like any good repo, your generator should have a great `README.md`(like this one) which acts as the documentation for your generator. Over time we're going to automate the creation of a preview image, like the one you see below, which'll give you a good idea of what you should expect to see from a generator.

Generators are just code, so you're free to compile and run them wherever they're compatible. This generator is a .Net Standard 2.0 library written in C# which means you can use it in a Revit addin, a Unity app, or as a "zero touch" library in Dynamo. But if you really want to put your generator to work, you can publish it to run on the Hypar platform, making it globally available and executable via Hypar's API. You can see this generator running [here](https://hypar.io/functions/hypar-dotnet-starter).  

<img src="https://github.com/hypar-io/starter/raw/master/preview.png" width="512px">

## Getting Started Developing for the Hypar Platform
The [Elements library](https://github.com/hypar-io/elements) is at the heart of the Hypar platform. You author the generator logic referencing the Elements library, and publish the generator to Hypar, then Hypar executes it for you and stores the results. Here's a very high level diagram of what happens:  

<img src="https://github.com/hypar-io/generator/raw/master/generator.png" width="300px">

You can see some generators written using Hypar Elements running on [Hypar](https://hypar.io). Hypar is just one example of a business that can be built on top of this tool. We fully expect you'll go and build your own cool thing.

- Go to https://www.hypar.io/ and sign up.
- Install [.NET](https://www.microsoft.com/net/)
- Install a good integrated development environment (IDE). We recommend [Visual Studio Code](https://code.visualstudio.com/) with the [C# for Visual Studio Code Extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp). [Visual Studio Community](https://visualstudio.microsoft.com/vs/community/) is also a great choice.
- Install the Hypar CLI:
  - Download for:
    - [Windows](https://s3-us-west-1.amazonaws.com/hypar-cli/hypar-win-x64.zip)
    - [Mac](https://s3-us-west-1.amazonaws.com/hypar-cli/hypar-osx.10.12-x64.zip)
    - [Linux](https://s3-us-west-1.amazonaws.com/hypar-cli/hypar-linux-x64.zip)
      - Linux requires that additional dependencies be installed to support .net. Those can be found [here](https://docs.microsoft.com/en-us/dotnet/core/linux-prerequisites?tabs=netcore21#linux-distribution-dependencies).
  - Make the CLI available on your command line by putting it in your path or making a symbolic link:
    - On Mac and Linux: `ln -s <path to hypar executable> /usr/local/bin/hypar`
    - On windows add `<path to hypar>` to your user `PATH`.
- Create a generator from the command line:
```
hypar init <generator id>
```
This will clone the generator repo to the folder `<generator id>`. Of course, you can replace `<generator-id>` with anything you like. The generator project is a buildable .net class library which references the Elements [NuGet package](https://www.nuget.org/packages/Hypar.Elements/).
- Edit the `hypar.json`. The `hypar.json` file describes the interface for your generator. At the top of the `hypar.json` file, the `hypar-schema` is referenced. In Visual Studio Code you'll get code completion and documentation as you author the `hypar.json`.
- Use the CLI to generate input and output classes and a function stub. From the same directory as your `hypar.json` do:
`hypar init`. This will generate `Input.gs.cs` and `Output.g.cs` classes which have properties which match your input and output properties. Addtionally, it will generate a `<function-id>.g.cs` whose `Execute(...)` method is where you put your business logic.
- Build
```
dotnet build
```
- Use the Hypar CLI to publish your function.
```
cd <function directory>
hypar publish
```
- Preview `.glb` models generated by Hypar locally using the [glTF Extension for Visual Studio Code](https://github.com/AnalyticalGraphicsInc/gltf-vscode), or [Don McCurdy's online glTF Viewer](https://gltf-viewer.donmccurdy.com/).

## Testing
```
cd test
dotnet test
```
