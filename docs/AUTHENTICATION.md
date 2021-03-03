### Table of Contents
- [Authentication](#authentication)
  * [Authentication using existing browser session](#authentication-using-existing-browser-session)
  * [Authentication using environment variable](#authentication-using-environment-variable)
  * [Authentication with credentials](#authentication-with-credentials)
  * [Switching to other Zeplin accounts](#switching-to-other-zeplin-accounts)

# Authentication

In this guide, we'll talk about how to authenticate using the Zeplin CLI.

CLI commands will automatically prompt you to authenticate if the command requires so, otherwise you can always use `zeplin login` command to authenticate without taking any action. There are 3 ways to authenticate:

## Using existing browser session

This is the default authentication flow.

1. Run the following command on terminal.

```sh
zeplin login
```

By default, Zeplin CLI will open a browser window to use your existing Zeplin session. If you are not already logged into the web app, you will be asked to login using your Zeplin credentials or an SSO provider.

2. The browser window should look like this, simply click on `Connect to Zeplin CLI`.<img src="../img/zeplinAuthentication.png" alt="Authenticate in Zeplin" width="500" />
3. Now head back to the terminal and the CLI will automatically log you in. If it does not, you can always copy token shown on the authentication page and paste it to the terminal prompt to proceed.

## Using environment variable

Zeplin CLI can authenticate using an access token instead of your Zeplin credentials which makes it easier to integrate it into your CI workflow.

1. Get a CLI access token from your [Profile](https://app.zeplin.io/profile/connected-apps) in Zeplin. If a CLI token already exists, you should first revoke the existing token and then generate a new one.
2. Set the `ZEPLIN_ACCESS_TOKEN` environment variable in your CI pipeline.

To login using other methods, simply unset the environment variable.

## Using account credentials

You can also use your Zeplin username/password to authenticate.

1. Run the following command on terminal.
```
zeplin login --no-browser
```
2. Type in your username and password.

## Switching to other Zeplin accounts

Run `zeplin login` again to authenticate with another Zeplin account.

Please note that the default login flow will automatically use the existing Zeplin session on your browser. You should first login with the other account on the Web app or use the [Authentication with credentials](#authentication-with-credentials) method to enter the other account's credentials.
