### Table of Contents
- [Quick Start with Connected Components](#getting-started-with-connected-components)
  * [Table of Contents](#table-of-contents)
  * [Requirements](#requirements)
  * [Connecting the first component](#connecting-the-first-component)
    + [Project types](#project-types)
  * [Inspect the configuration file](#inspect-the-configuration-file)
  * [Update Connected Components](#update-connected-components)
  * [Connecting more components](#connecting-more-components)
    + [Using CLI command](#using-cli-command)
    + [Using VS Code Extension](#using-vs-code-extension)
  * [Add links (Optional)](#add-links-optional)
- [Troubleshooting](#troubleshooting)

# Quick Start with Connected Components

This guide covers how to get started with Connected Components for React, Angular, Vue.js interactively.

## Requirements

[node 10+](https://docs.npmjs.com/downloading-and-installing-node-js-and-npm) must be installed on your system.

## Connecting the first component

Open Zeplin, navigate to the components page of our project or styleguide and select a component that we want to connect.

<img src="../../img/zeplinConnectToCode.png" alt="Click on Connect To Code button" width="800" />

We click on _Connect to Code_ button. Now, Zeplin will show us a command sample to connect this component. While `--project-id <projectId>` or `--styleguide-id <styleguideId>` parameters are based on what Zeplin resource we are navigating, `--component-id <componentId>` represents the component we have selected.

Clicking on the command will copy it to the clipboard.

<img src="../../img/zeplinConnectToCodePrompt.png" alt="Connected Components initialize command" width="800" />

Open a terminal and navigate to the source code project folder, paste and execute the command.

```sh
npx @zeplin/cli connect initialize \
    --project-id 5e53a7928b7751764c16eee5 \
    --component-id 5dd417142dff493fc295dda1
```

We follow the instructions, CLI will ask us to authenticate(../lin/) and select a component file. Finally, CLI will create `.zeplin/components.json` file in our project and install required the packages.

<img src="../../img/zeplinInitialization.gif" alt="Initialize flow" width="800" />

**Congratulations, we just connected our first component!** 🎉

Now we can go back to Zeplin and see that our component enriched with links! Based on our project type, the component may have a description and code snippet.

<img src="../../img/zeplinConnectedComponent-react.png" alt="Connected component" width="800" />

### Project types

Initialize command can detect the project type and install related CLI plugins and enrich Connected Components even more. As of now, the following project types are supported. Check the links for configuration details about each plugin.
 - [React](https://github.com/zeplin/cli-connect-react-plugin)
 - [Angular](https://github.com/zeplin/cli-connect-angular-plugin)
 - [Vue.js](https://github.com/johntips/storybook-vue-zeplin)
 - [Storybook](https://github.com/zeplin/cli-connect-storybook-plugin)

## Inspect the configuration file

Open `.zeplin/components.json` on your source code project. Its content will be something similar to the below example.

```json
{
    "plugins": [
        {
            "name": "@zeplin/cli-connect-react-plugin"
        },
        {
            "name": "@zeplin/cli-connect-storybook-plugin",
            "config": {
                "url": "http://localhost:9009",
                "startScript": "storybook"
            }
        }
    ],
    "projects": [
        "5e53a7928b7751764c16eee5"
    ],
    "components": [
        {
            "path": "src/components/button/Button.jsx",
            "zeplinIds": [
                "5dd41717b4eaa04034df4c6f"
            ]
        }
    ]
}
```

- `projects` and `styleguides` keys are the identifiers of projects and styleguides we'll use components from.
- `plugins` contain the module name of the plugins, which should be invoked while CLI processing our components. Each plugin may have its own custom configuration under `config` key.
- `components` are the React component files in our codebase. `zeplinIds` are the component IDs in Zeplin that CLI will connect the component file. We may alternatively use deprecated `zeplinNames` field instead of `zeplinIds` to connect components.

Check [CONFIGURATION_FILE.md](../CONFIGURATION_FILE.md) for more details.

## Update Connected Components

Executing `zeplin connect` (or `npm run zeplin-connect` if Zeplin CLI packages are installed locally) will process the configuration/component files again, and update our Connected Components on Zeplin.

We may add a task into our CI/CD pipeline to update Connected Components every time a change has happened on our source code.

## Connecting more components

After we initialize Connected Components, we can use `zeplin connect add-components` (or `npm run zeplin-connect add-components` if Zeplin CLI packages are installed locally) command to connect more components to Zeplin interactively.

It is possible to add components from other Zeplin projects or styleguides into the same configuration file. If you're using [Global Styleguides](https://blog.zeplin.io/announcing-global-styleguides-connecting-design-systems-to-engineering-65ad22bd0076), adding your components using IDs of styleguide(s) will be enough. The connected component will show up on the parent Zeplin project or styleguide(s) as well.

### Using CLI command

Open Zeplin and select a component that is not connected yet. Click on _Connect to Code_ button again. This time, Zeplin will us the command add this component to the existing Connected Component configuration (Notice that the only difference is `add-components` instead of `initialize`)

Paste and execute the command on our source code project. CLI will add this project or styleguide and the component to `.zeplin/component.json` file

```sh
npx @zeplin/cli connect add-components \
    --project-id 5e53a7928b7751764c16eee5 \
    --component-id 5dd417142dff493fc295dce5
```

Rinse and repeat until connecting all components!

_Using `initialize` command will fallback to `add-components` if you have an existing `.zeplin/components.json` and vice versa._

### Using VS Code Extension

We can use [Zeplin Visual Studio Code extension](https://zpl.io/vscode-extension) to manage the `.zeplin/components.json` file. It simplifies adding more components into the configuration configure and connect more
components.

The extension will detect the existence of `.zeplin/components.json` file automatically.
- Open the file in VSCode, notice that there are code lens actions on the configuration fields
<img src="../../img/zeplinVSCodeExtension.png" alt="Zeplin VSCode Extension" width="800" />
- Click the _Add component_ link which will list all the files in your repository, and then select the file. Extension will add a new component object into the configuration file.
- Click _Connect to Zeplin component_ on the created component, it will show all commponents in your project or styleguidein Zeplin. We may search for a component name, and select multiple components for a single component.


## Add links (Optional)

Connected Components also lets you add links to various sources like your Storybook, repository, wiki and so on. In the screenshot above, notice that we have links to GitHub and Storybook.

Zeplin CLI will try to configure Storybook and git repository automatically, if it couldn't for your source code project, check out these guides to add links:

- [Adding Storybook links](../link/STORYBOOK.md)
- [Adding Styleguidist links](../link/STYLEGUIDIST.md)
- [Adding repository links](../link/REPOSITORY.md), e.g. GitHub, GitLab, Bitbucket
- [Adding custom links](../link/CUSTOM.md), e.g. internal Design System wiki

# Troubleshooting

Check [Troubleshooting](../TROUBLESHOOTING.md) document for common issues.