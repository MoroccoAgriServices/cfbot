# cfbot

[Cloud Foundry](http://cloudfoundry.org) application monitoring bot for
[Slack](https://slack.com).

cfbot monitors application events through the [CF events API] and forwards
details to channels it's registered in. Users can configure the applications
and events being monitored.

The following events are currently registered:

* App Creation and Deletion Events.
* App Lifecycle Events (start, stop, restart, restage)
* Instance Crash Events. 
* Scaling (memory, CPU, disk)
* Routes Changes (map, unmap)

<a href="https://bluemix.net/deploy?repository=https://github.com/jthomas/cfbot" target="_blank">
<img src="http://bluemix.net/deploy/button.png" alt="Bluemix button" />
</a>

PICTURE

## install 

This Cloud Foundry monitoring bot can be deployed to... Cloud Foundry!

You will need to register the bot with your Slack group to receive an
authentication token. This token, along with login details for 
a platform account, need to be created as user-provided service credentials.
The bot will read these service credentials on deployment and start monitoring
for events.

Follow the steps below for details...

### register slack bot 

Add a new bot integration [here](https://slack.com/services/new/bot) with the
following details:

* *username:* _cf_

Make a note of the API token.

*tip: grab the cloud foundry logo for your bot picture from [here](https://twitter.com/cloudfoundry)*

### create user provided service credentials 

Create user-provided service credentials on the Cloud Foundry
instance where you will be deploying cfbot using the command below.

You need to provide the API token from Slack, the Cloud Foundry endpoint running
the applications you want to monitor and user account credentials for that
platform. 

*tip: create a new user account for cfbot and add it to your cf organisation to expose applications 
for monitoring, rather than having to use normal user accounts.*

<pre>
cf cups cfbot -p '{"slack_token":"xoxb-some-token","cf_api":"https://api.ng.bluemix.net", "cf_username":"xxx", "cf_password":"xxx"}'
</pre>

### deploy 

<pre>
$ cf push
</pre>

## usage 

cfbot will monitor events from applications in all spaces and
organisations that the user account has access to. 

Users can filter the applications and events being reported using the *apps* and
*events* commands. Both commands take application or event identifiers that are
used to match incoming events. The wildcard '*' identifier can be used to revert
to matching all events.

<pre>
@cf apps // show the currently application filter
@cf apps app_name // add the 'app_name' to the filter list
@cf apps * // reset to the filter to wildcard matching

@cf events // show the currently event filter
@cf events event_type // add the 'event_type' to the filter list
@cf events * // reset to the filter to wildcard matching

@cf status // show the current bot status message
</pre>

# bugs / feedback / comments

Open [issues](https://github.com/jthomas/cfbot/issues) or find me on [twitter](http://twitter.com/thomasj).
Pull requests welcome!
