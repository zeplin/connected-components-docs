### Table of Contents

- [Troubleshooting](#troubleshooting)
  * [Authentication](#authentication)
    + [I want to switch to another account but CLI keeps using the same Zeplin account](#i-want-to-switch-to-another-account-but-cli-keeps-using-the-same-zeplin-account)
    + [Permission errors](#permission-errors)
  * [Components](#components)
    + [Components not found](#components-not-found)
  * [Storybook](#storybook)
    + [Storybook links are not found](#storybook-links-are-not-found)
    + [Storybook is opened but cannot be loaded when I click on Storybook links](#storybook-is-opened-but-cannot-be-loaded-when-i-click-on-storybook-links)
    + [I am getting SSL errors while connecting to my Storbook instance](#i-am-getting-ssl-errors-while-connecting-to-my-storbook-instance)
    + [My Storybook instance is behind Basic authentication proxy](#my-storybook-instance-is-behind-basic-authentication-proxy)

# Troubleshooting

## Authentication

### I want to switch to another account but CLI keeps using the same Zeplin account

Check [Switching to other Zeplin accounts](./AUTHENTICATION.md#switching-to-other-zeplin-accounts) to learn more about authenticating with another account.

### Permission errors
If you're a part of a workspace, the role of the Zeplin account must be Developer or higher.

If you are getting permission errors regardless of your role, please check that if your account joined to the project or the styleguide that you are trying to connect.

## Components

### Components not found

The plugin you are using could not parse or find a definition of a component. This is a common issue for React component as there are many ways to compose a component and some of these methods are not supported by `react-docgen` or `react-docgen-typescript`. Please check [React plugin documentation for details](https://github.com/zeplin/cli-connect-react-plugin).

## Storybook

### Storybook links are not found

Please see the [Matching components with stories](https://github.com/zeplin/cli-connect-storybook-plugin#matching-components-with-stories) document.

### Storybook is opened but cannot be loaded when I click on Storybook links

This can happpen when you are using Storybook v5+ but the links are not generated using v5+ format. To resolve it please see the [URL format for manual matching](https://github.com/zeplin/cli-connect-storybook-plugin#url-format-for-manual-matching) document.

### I am getting SSL errors while connecting to my Storbook instance

This can happen if the Storybook instance is served over HTTPS with a self-signed or an intermediate certificate. Currently we don't support custom certificates to connect Storybook but you can [configure Storybook plugin to ignore SSL errors](https://github.com/zeplin/cli-connect-storybook-plugin#ignore-ssl-certificate-errors).

### My Storybook instance is behind Basic authentication proxy

Please see the [Using Basic Authentication](https://github.com/zeplin/cli-connect-storybook-plugin#ignore-ssl-certificate-errors) document.
