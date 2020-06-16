# Issue Status

Simple status page built using React and GitHub Issues

![Banner](/banner.gif?raw=true)

### Demo

You can view the Issue Status demo [here](https://tadhglewis.github.io/issue-status). This demo is hosted on GitHub Pages

### Features

- Easy setup
- Component reporting to show the current status of your services
- Incident reporting
- Hosting on GitHub Pages or other hosting providers
- Live updating status page
- Use Zapier Triggers to update the status page
- Easy integration with services and monitoring

### Setup

- Clone / Fork this repository to your GitHub account (forking only required for GitHub Pages)
- Edit the `package.json` file and update `homepage`. You should enter the URL you are using for the status page
- Edit the `config.js` file found in `src/config.js` and enter your GitHub username in the `user` field. [Configuration options](#configuration)

GitHub Pages

- Run `npm run deploy` this will build the React project and deploy it to the `gh-pages` branch
- Finally make sure GitHub Pages option in your GitHub repository settings is set to use the `gh-pages` branch

Other hosting providers

- Run `npm run build` this will create a build directory containing the built app
- For deploying [click here](https://create-react-app.dev/docs/deployment)

### Updating

Updating is important to get the latest features and patches

- [This guide](https://help.github.com/en/github/collaborating-with-issues-and-pull-requests/syncing-a-fork) should bring you through the steps of syncing your forked version of this repository

GitHub Pages

- Run `npm run deploy` to deploy the latest version to GitHub Pages

Other hosting providers

- Run `npm run build` to create a new build directory
- For deploying [click here](https://create-react-app.dev/docs/deployment)

### Advanced

Integrate and automate Components and Incidents, this may be useful for changing a Component to `major outage` when you detect your services aren't running or `performance issues` when the response time goes over a set point.

- Issue Status API (GitHub API wrapper) - [In the future](https://github.com/tadhglewis/issue-status/issues/18), there will be a GitHub API wrapper which can be hosted on a server. This will expose simplified endpoints for integrating with monitoring services, IFTTT and any other services
- [IFTTT](https://ifttt.com) - This is currently not possible due to a couple issues. 1. GitHub service does not include labels in the create Issue action. 2. The GitHub service does not have an update Issue action. It is also not possible to call the GitHub API directly as IFTTT does not include a User-Agent header in the Webhooks service and [all requests with no User-Agent header will be rejected by the GitHub API](https://developer.github.com/v3/#user-agent-required). This is possible using the Issue Status API
- [Zapier](https://zapier.com) - You can create Zaps which have a trigger and an action, use the GitHub Integrations action to update/created Components and Incidents with any of the Zapier Triggers
- [GitHub API](https://developer.github.com) - You can use the GitHub API directly, you can use this for more advanced options

### Configuration

package.json

- `homepage` - Determines the root URL in the built HTML file. You should enter the URL you are using for the status page

config.js (src/config.js)

- `logo` - Accepts an image URL and is used in the status page header. Ensure the image size is correct
- `name` - Used when no `logo` is provided and is used in the status page header. This will be used in the img alt attribute if a logo is provided
- `user` - GitHub username that Component and Incidents will be fetched from

### Details

In depth overview of the functionality

- The main status bar logic is as follows: < 70% Components `operational` = "Some systems are experiencing issues", more than 0 Components `major outage` = "Some systems are experiencing a major outage". Otherwise, "All Systems Operational"
- A `Component` each display a current status. To create a Component add tags `issue status`, `component` and a tag for the current status: `operational`, `performance issues`, `partial outage` or `major outage` (if an issue only has `issue status` and `component` it will be listed as `Unknown`) to a GitHub Issue. You can view all the demo Components [here](https://github.com/tadhglewis/issue-status/issues?q=is%3Aissue+label%3A%22issue+status%22+label%3A%22component%22)
- A `Incident` will show in the Incidents section as either `Active` or `Closed` depending whether on the GitHub Issue is Open or Closed. To create an Incident add tags `issue status` and `incident` to a GitHub Issue. You can view all the demo Incidents [here](https://github.com/tadhglewis/issue-status/issues?q=is%3Aissue+label%3A%22issue+status%22+label%3A%22incident%22)
- Issue Status uses the [GitHub API v3](https://developer.github.com/v3) which has a rate limit of 60 requests per hour for unauthenticated requests (Issue Status is client side and will use unauthenticated requests). Issue Status will fetch 15 times per hour, sending 2 requests per fetch / 30 requests per hour (excluding reload button)

If you have any issues or questions feel free to contact me

### Version

0