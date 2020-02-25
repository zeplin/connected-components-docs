# Adding custom links

In this guide, we'll talk about how to add custom links to components. This lets you display links to various sources in Zeplin, e.g. your documentation on Confluence, public design system website, wiki on Notion and so on.

It doesn't matter whether these links are internal to your company or accessible to public, since Zeplin will simply displaying a button that opens the link in your browser.

☝️ _If you haven't created a Connected Components configuration file yet, check out our [getting started guides](/README.md#getting-started)._

In this example, we'll add links to our design system documentation on (1) Confluence and (2) Notion. Here's our sample configuration file with two components and no links at all:

```json
{
    "plugins": [
        {
            "name": "@zeplin/cli-connect-react-plugin"
        }
    ],
    "projects": [],
    "styleguides": [
        "5cd486b18a64c1414be004fb"
    ],
    "components": [
        {
            "path": "src/components/Button/Button.jsx",
            "zeplinNames": [
                "Controls / Button / Primary"
            ]
        },
        {
            "path": "src/components/TextField/TextField.jsx",
            "zeplinNames": [
                "Controls / Text field / Primary"
            ]
        }
    ]
}
```

## Adding the first custom link

Firstly, in our configuration file, we'll add a property called `links`. `links` property is a list that can hold multiple links but we'll first define our Confluence link like so:

```json
{
    …
    "components": [
        …
    ],
    "links": [
        {
            "name": "Confluence",
            "type": "confluence",
            "url": "https://example.atlassian.net/wiki/spaces/DS/pages"
        }
    ]
}
```

While defining a link, we need to provide 3 properties:

1. `name` property is the name for the link that'll be displayed in Zeplin. In this case, we put in “Confluence” so that the button in Zeplin would say “Open in Confluence”.
2. `type` property is an identifier that will not be displayed in Zeplin at all. We'll use this identifier in a bit while defining the URL path for a particular component.
3. `url` property is where we specify the base URL. Note that this is not a complete URL but only the shared piece of URL across all of our components. For a component with URL `https://example.net/design-system/Button`, the base URL would probably be `https://example.net/design-system`.

Let's now define the URL paths for the two components in our configuration file. To do that, under each component, we'll add a property called `confluence`, which refers to the identifier we just defined in the `type` property. Finally, within this `confluence` property, we'll define the URL path under the `urlPath` property, like so:

```json
{
    …
    "components": [
        {
            "path": "src/components/Button/Button.jsx",
            "zeplinNames": [
                "Controls / Button / Primary"
            ],
            "confluence": {
                "urlPath": "260407436/Button"
            }
        },
        {
            "path": "src/components/TextField/TextField.jsx",
            "zeplinNames": [
                "Controls / Text field / Primary"
            ],
            "confluence": {
                "urlPath": "260407439/Text+field"
            }
        }
    ],
    "links": [
        {
            "name": "Confluence",
            "type": "confluence",
            "url": "https://example.atlassian.net/wiki/spaces/DS/pages"
        }
    ]
}
```

Zeplin concatenates the URL path of the component to the base URL based on the `type` property. So for the button component, the complete URL ends up being `https://example.atlassian.net/wiki/spaces/DS/pages/260407436/Button`.

This is it! Now when we run `zeplin connect`, we should start seeing the “Open in Confluence” button in Zeplin:

<img src="../../img/zeplinCustomLink.png" alt="Connected component in Zeplin" width="314" />

## Adding multiple custom links

It is also possible to define multiple custom links under the `links` property. Let's define a link to Notion as well, along with our Confluence link, which would look like so:

```json
{
    …
    "components": [
        …
    ],
    "links": [
        {
            "name": "Confluence",
            "type": "confluence",
            "url": "https://example.atlassian.net/wiki/spaces/DS/pages"
        },
        {
            "name": "Notion",
            "type": "notion",
            "url": "https://www.notion.so/example"
        }
    ]
}
```

Similar to Confluence, we'll now define the URL paths for Notion. Note that we don't have to define a URL path for each component. Zeplin will only display the “Open in Notion” button for the ones that do have a URL path. To demonstrate this, let's add the Notion URL path only for the text field component, like so:

```json
{
    …
    "components": [
        {
            "path": "src/components/Button/Button.jsx",
            "zeplinNames": [
                "Controls / Button / Primary"
            ],
            "confluence": {
                "urlPath": "260407436/Button"
            }
        },
        {
            "path": "src/components/TextField/TextField.jsx",
            "zeplinNames": [
                "Controls / Text field / Primary"
            ],
            "confluence": {
                "urlPath": "260407439/Text+field"
            },
            "notion": {
                "urlPath": "Text-field-ab17d54d86f547e5bee6ae62e67073a4"
            }
        }
    ],
    "links": [
        …
    ]
}
```

Now when we run `zeplin connect`, we should see both “Open in Confluence” and “Open in Notion” buttons for the text field component, but only see the “Open in Confluence” button for the button component.

Hope this quick guide on custom links was helpful, reach out to us at [support@zeplin.io](mailto:support@zeplin.io) if you have questions or feedback.
