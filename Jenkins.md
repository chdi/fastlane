# Jenkins Integration

`fastlane` automatically generates a JUnit report for you. This allows Continuous Integration systems, like `Jenkins`, access the results of your deployment.

## Installation
The recommended way to install [Jenkins](http://jenkins-ci.org/) is through [homebrew](http://brew.sh/):

```brew update && brew install jenkins```

From now on start ```Jenkins``` by running:
```
jenkins
```

To store the password in the Keychain of your remote machine, I recommend running `sigh` or `deliver` using ssh or remote desktop at least once.

## Deploy Strategy

You should **not** deploy a new App Store update after every commit, since you still have to wait 1-2 weeks for the review. Instead I recommend using Git Tags, or custom triggers to deploy a new update.

You can set up your own ```Release``` job, which is only triggered manually.

## Plugins

I recommend the following plugins:

- **[HTML Publisher Plugin](https://wiki.jenkins-ci.org/display/JENKINS/HTML+Publisher+Plugin):** Can be used to show the generated screenshots right inside Jenkins.
- **[AnsiColor Plugin](https://wiki.jenkins-ci.org/display/JENKINS/AnsiColor+Plugin):** Used to show the coloured output of the fastlane tools. Dont' forget to enable `Color ANSI Console Output` in the `Build Environment` or your project.
- **[Rebuild Plugin](https://wiki.jenkins-ci.org/display/JENKINS/Rebuild+Plugin):** This plugin will save you a lot of time.

## Build Step
Use the following as your build step:
```
fastlane appstore
```
Replace `appstore` with the lane you want to use.

## Test Results and Screenshtos

To show the **deployment result** right in `Jenkins`

- *Add post-build action*
- *Publish JUnit test result report*
- *Test report XMLs*: `fastlane/report.xml`

To show the **generated screenhots** right in `Jenkins`

- *Add post-build action*
- *Publish HTML reports*
- *HTML directory to archive*: `fastlane/screenshots`
- *Index page*: `screenshots.html`

Save and run. The result should look like this:

![JenkinsIntegration](assets/JenkinsIntegration.png)