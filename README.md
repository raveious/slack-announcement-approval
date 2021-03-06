# Announcement Approval for Slack [![Build Status](https://travis-ci.org/trianglefraternitymtu/slack-announcement-approval.svg?branch=master)](https://travis-ci.org/trianglefraternitymtu/slack-announcement-approval) [![Installs](https://slack-announcement-approval.herokuapp.com/badge/installs)](https://slack-announcement-approval.herokuapp.com/)

This is for teams where posting to the [#general][1] channel (often renamed to [#announcements][2] has been restricted to team owners and/or admins. This would allow a user to have a message posted to the [#general][1] channel after getting approval from an admin or another private channel.

## Setup

<a href="https://slack.com/oauth/authorize?scope=commands,channels:read,groups:read,users:read,chat:write:bot&client_id=19225015925.110455013810&state=appAdded"><img alt="Add to Slack" height="40" width="139" src="https://platform.slack-edge.com/img/add_to_slack.png" srcset="https://platform.slack-edge.com/img/add_to_slack.png 1x, https://platform.slack-edge.com/img/add_to_slack@2x.png 2x" /></a>

After the app is added to your team, you will be asked to sign in with Slack.

<a href="https://slack.com/oauth/authorize?scope=identity.basic,identity.team&client_id=19225015925.110455013810&state=resumeSignIn"><img alt="Sign in with Slack" height="40" width="172" src="https://platform.slack-edge.com/img/sign_in_with_slack.png" srcset="https://platform.slack-edge.com/img/sign_in_with_slack.png 1x, https://platform.slack-edge.com/img/sign_in_with_slack@2x.png 2x" /></a>

You will then be sent to the configuration page for your team.

Note: By default, only team admins and owners are allowed to edit the team configuration. Everyone else will be denied access until an admin or team owner logs in and allows everyone access.

## Usage

With no further configuration, the app has been added to your team once its added to the team.

### Making a request

Anyone can make a request to make an announcement using this slash command, `/announce` followed by your message. All Markdown and emojis will work as normal and will be passed on as if you had posted the announcement yourself.

![Slash command definition](website/static/slash_command.jpg)

Due to the fact that Slack bots are able to use `@here`, `@channel` and `@everyone` regardless of team settings, adding them to your message will work as normal and will trigger the appropriate notification in the channel it gets posted to. Simply add the correct string, as if you can use it normally and even if it doesn't show up in your quick select popup, it will still work as if you could normally.

### Handling a request

In the selected channel to post the requests for approval, a message like this one will be posted. These buttons are interactable and simply clicking `Approve` or `Reject`.

![Button prompt](website/static/button_prompt.jpg)

This example was made using `/announce This is the *body* of a request :clap:`

Once the post has been approved or rejected, the prompt will update to record who addressed it and when it was addressed.

### Processed response

If the message was rejected, the individual who make the initial request will get this message to inform them that their announcement won't be made. This message will be a direct message from `@slackbot`. Furthermore, you have the option to block the user from making another request for some duration of time by selecting the time from the menu.

![Rejected](website/static/rejected.jpg)

If the message was approved, a post will be made automatically to selected channel. The bot will use the icon and real name of the individual who made the request in the first place. This is to show who wanted to make the announcement.

### Diverting the response

There is a menu with all the channels in it to give you the choice to divert the message to any channel in the list. This gives the team admins another option to push the message to a lower channel instead of just rejecting it.

The diverted post will look exactly the same, as if it approved, just in the selected channel.

## Configuration

At the configuration page, these are the available settings that can be changed for your Slack team. To get to the configuration page, you simply need to signin with Slack.

Option | Default Value | Description
:---|:---:|:---:
Post channel | [#general][1] or it's replacement | The selected channel that is ultimatly trying to be posted too. This has to be a public channel.
Approval channel** | The user who added the app to the team | The channel where an post needs approval from. Typically a "Executive Board" kind of channel that is typically private.
Admin only approval | True | In the channel that the request will be sent to, allow only a team admin to respond. This is for the case where there are both team admins and non-admins in the approval channel.
Admin only login | True | Only an admin can change these settings. This can be disabled, but requires and team admin or owner to login to disable it.

** This list is determined by the user who added the app to the team in the first place. If you have a dummy account to just hold authentication tokens, this user would also have to be in the private channel you want to select.

[1]: https://my.slack.com/messages/general/ "#general"
[2]: https://my.slack.com/messages/announcements/ "#announcements"
[3]: https://slack.com/oauth/authorize?scope=identity.basic,identity.team&client_id=19225015925.110455013810&state=resumeSignIn "signin"
