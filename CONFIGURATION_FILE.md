# Configuration file

## Properties

| Property | Type | Description |
| --- | --- | --- |
| `projects` | `string[]` | Identifiers of projects to add components from |
| `styleguides` | `string[]` | Identifiers of styleguides to add components from |
| `components` | [`Component[]`](#Component) | Component files in codebase, with connections to Zeplin counterparts |
| `plugins` | [`Plugin[]`](#Plugin) _(Optional)_ | Plugins to use with [Zeplin CLI](https://github.com/zeplin/cli) |
| `links` | [`Link[]`](#Link) _(Optional)_ | Base URLs for custom component links, e.g. wiki |
| `github` | [`RepositoryConfig`](#RepositoryConfig) _(Optional)_ | Configuration for GitHub component links |
| `gitlab` | [`RepositoryConfig`](#RepositoryConfig) _(Optional)_ | Configuration for GitLab component links |
| `bitbucket` | [`RepositoryConfig`](#RepositoryConfig) _(Optional)_ | Configuration for Bitbucket component links |

## Models

### `Component`

A component file in the codebase, with connections to Zeplin counterparts.

| Property | Type | Description |
| --- | --- | --- |
| `path` | `string` | File path of the component |
| `name` | `string` _(Optional)_ | Custom name of the component to be displayed in Zeplin |
| `zeplinNames` | `string[]` | Names of the components in Zeplin to connect to |
| `storybook` | [`StorybookConfig`](#StorybookConfig) _(Optional)_ | Configuration for Storybook plugin, only for manually matching components with stories—to learn more, check out [Storybook plugin documentation](https://github.com/zeplin/cli-connect-storybook-plugin/) |
| `styleguidist` | [`StyleguidistConfig`](#StyleguidistConfig) _(Optional)_ | Configuration for Styleguidist link

☝️ _Components can have additional custom properties based on the plugins you use._

### `Plugin`

A plugin to use with [Zeplin CLI](https://github.com/zeplin/cli).

| Property | Type | Description |
| --- | --- | --- |
| `name` | `string` | npm package name of the plugin, e.g. `@zeplin/cli-connect-react-plugin` |
| `config` | `string` _(Optional)_ | Configuration for the plugin—see plugin's documentation to learn more |

### `Link`

A base URL for a custom component link, e.g. wiki.

| Property | Type | Description |
| --- | --- | --- |
| `name` | `string` _(Optional)_ | Name of the link to be displayed in Zeplin |
| `type` | `string` | Custom type for a link you define, e.g. `wiki` |
| `url` | `string` | Base URL of the link, e.g. `https://wiki.example.com/design-system` |

Once you define a link, you can set the URL paths for each component like so:

```json
{
    …
    "components": [
        …,
        {
            "name": …,
            "path": …,
            "zeplinNames": [
                …
            ],
            "wiki": {
                "urlPath": "components/button"
            },
            "public": {
                "urlPath": "components/button"
            }
        },
        …
    ],
    "links": [
        {
            "name": "Internal Wiki",
            "type": "wiki",
            "url": "https://wiki.example.com/design-system"
        },
        {
            "name": "Public Design System Documentation",
            "type": "public",
            "url": "https://design.example.com/"
        }
    ]
}
```

### `RepositoryConfig`

Configuration for repository links, e.g. GitHub, GitLab, Bitbucket.

| Property | Type | Description |
| --- | --- | --- |
| `repository` | `string` | Name of the repository to link to, e.g. `example/react-components` |
| `branch` | `string` _(Optional)_ | Branch of the repository to link to—defaults to `master` |
| `url` | `string` _(Optional)_ | Base URL, e.g. if using GitHub Enterprise |
| `path` | `string` _(Optional)_ | Path of the project, if you're using a monorepo |

### `StorybookConfig`

Configuration for Storybook plugin, only for manually matching components with stories—to learn more, check out [Storybook plugin documentation](https://github.com/zeplin/cli-connect-storybook-plugin/).

| Property | Type | Description |
| --- | --- | --- |
| `kind` | `string` | Name defined in component's `.stories.js` file |
| `stories` | `string[]` | Names of stories defined in component's `.stories.js` file |

### `StyleguidistConfig`

Configuration for Styleguidist component links.

| Property | Type | Description |
| --- | --- | --- |
| `kind` | `string` | Name of the component used in the Styleguidist URL, after `#` |
