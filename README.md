# Replicate 💾

Create projects from templates. It may be for app development, frameworks, ios apps and android apps. This is just an utility CLI which helps you
- fetch a template
- replace strings in filenames and inside files

Here's a template we're working on

- [hfossli/replicate-ios-app](https://github.com/hfossli/replicate-ios-app)

## Installation

### Download, compile and install
```
cd ~/Downloads && curl -L https://github.com/hfossli/Replicate/archive/master.zip | tar zx && cd Replicate-master && make
```

Then you'll be able to run `replicate` from any folder. E.g.
```
replicate --template hfossli/replicate-ios-app
```

### Manually

You can either

- Run `./main.swift` in your terminal.

or

- Run `make` in your terminal to install Replicate.
- Run `replicate` in your terminal.

or

- Open `Replicate.xcodeproj`.
- Run the project, and use Xcode’s console to provide input.

or

- Open `Replicate.xcodeproj`.
- Archive the project.
- Move the built binary to `/usr/local/bin`.
- Run `replicate` in your terminal.

## Example

1. Install Replicate and paste this into terminal
```
replicate --template hfossli/replicate-ios-app --destination Foo
```
2. Answer the questions popping up
3. Open folder `Foo` and you'll see a project ready for development

## Options

You may use the guide to input information or you may pass options as arguments on launch. The Replicate program only has 3 options, but a template may ask for more.

### Replicate options

| Name        | Description                                 | Long parameter  |
|:------------|:--------------------------------------------|:----------------|
| Destination | Where the generated project should be saved | `--destination` |
| Template    | The location of your template               | `--template`    |
| Force       | Don't use the interactive mode              | `--force`       |

### Each template will have its own options

E.g. [hfossli/replicate-ios-app](https://github.com/hfossli/replicate-ios-app) can be used like so
```
main.swift --template hfossli/replicate-ios-app --destination FooBar --project-name "XYZFooBar" --company-name "The lot"
```

## Similar concepts

- [Toughtbot's liftoff](https://github.com/thoughtbot/liftoff)
- [SwiftPlate](https://github.com/JohnSundell/SwiftPlate)

Why don't you use [Toughtbot's liftoff](https://github.com/thoughtbot/liftoff) or [SwiftPlate](https://github.com/JohnSundell/SwiftPlate)? Simply because they're geared towards one specific setup.

## Creating templates

### Replicate.json

In the root directory of your template project add a file named `replicate.json` with some information about which strings you want replaced. Here's an example:
```
{
  "replace": [
    {
      "find": "R-PROJECT-NAME",
      "description": "What's the name of your project?",
      "suggestion": "folder.name"
    },
    {
      "find": "R-AUTHOR-NAME",
      "description": "What's your name?",
      "suggestion": "git.user.name"
    },
    {
      "find": "R-AUTHOR-EMAIL",
      "description": "What's your email address?",
      "suggestion": "git.user.email"
    },
    {
      "find": "R-COMPANY-NAME",
      "description": "What's your company name?"
    },
    {
      "find": "R-COMPANY-IDENTIFIER",
      "description": "What's your company identifier? E.g. \"no.agens\""
    }
  ]
}
```

Until we reach 1.0 this format is subject to change. After that it will only be additive features.

#### Replace

The replace dictionary may concist of following keys

###### find (required string)
Used to determine which strings to replace.

###### name (optional string)
If this is omitted we will derive the name from the "find" attribute. Used as argument name for CLI. E.g. setting `find` to `R-COMPANY-NAME` will make `--company-name` available as a CLI argument.

###### description (required string)
Text used by CLI to ask user for input.

###### optional (optional bool)
Is this optional or required?

###### suggestion (optional string)
As you may see in the "suggestion" attribute in json you can specify suggestions which are dynamic. We support

- git.user.email
- git.user.name
- folder.name
- date.year

###### hidden (optional bool)
Used in combination with `suggestion` to inject dynamic fields like `date.year` in copyright texts.

### Best practices

1. For strings you want replaced prefix them with `R-` e.g. `R-AUTHOR-NAME`
2. Only use `-` or characthers `A-Z`. E.g. don't name your project file `<%PROJECT%>.xcodeproj` as xcode will have a hard time dealing with that while developing your template. Instead name your project `R-PROJECT-NAME.xcodeproj`.


## About the name

This project is named `replicate` for 2 reasons:

1. [SwiftPlate](https://github.com/JohnSundell/SwiftPlate) is the big inspiration here and most of the code is shamelessly taken from that project. This is just a replica of [SwiftPlate](https://github.com/JohnSundell/SwiftPlate), but geared more towards supporting many different project structures instead of having just one.
2. It will replicate any template you specify as long as it has a replicate.json file

## Credits

All credits goes to [John Sundell](https://twitter.com/johnsundell) for creating [SwiftPlate](https://github.com/JohnSundell/SwiftPlate) with MIT license allowing us to repurpose that code.
