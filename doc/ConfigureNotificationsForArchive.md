OPTIONAL: You can choose to integrate with [Pushover](https://pushover.net), [Gotify](https://gotify.net/), [IFTTT](https://ifttt.com), and/or [AWS SNS](https://aws.amazon.com/sns/) to get a push/email notification to your phone when the copy process is done. Depending on your wireless network speed/connection, copying files may take some time, so a push notification can help confirm that the process finished. If no files were copied (i.e. all manually saved dashcam files were already copied, no notification will be sent.).

# Pushover
The Pushover service is free for up to 7,500 messages per month, but the [iOS](https://pushover.net/clients/ios)/[Android](https://pushover.net/clients/android) apps do have a one time cost, after a free trial period. *This also assumes your Pi is connected to a network with internet access.*

1. Create a free account at Pushover.net, and install and log into the mobile Pushover app.
1. On the Pushover dashboard on the web, copy your **User key**.
1. [Create a new Application](https://pushover.net/apps/build) at Pushover.net. The description and icon don't matter, choose what you prefer.
1. Copy the **Application Key** for the application you just created. The User key + Application Key are basically a username/password combination to needed to send the push.
1. Run these commands, substituting your user key and app key in the appropriate places. No `"` are needed.
    ```
    export pushover_enabled=true
    export pushover_user_key=put_your_userkey_here
    export pushover_app_key=put_your_appkey_here
    ```

# Gotify
Gotify is a self-hosted notification service. The android client is available on [Google Play](https://play.google.com/store/apps/details?id=com.github.gotify), [F-Droid](https://f-droid.org/de/packages/com.github.gotify/), or a standalone [APK](https://github.com/gotify/android/releases/latest).

1. Install server by following [instructions](https://gotify.net/docs/install)
1. [Create a new Application](https://gotify.net/docs/pushmsg)
1. Copy the app's token
1. Run these commands, substituting your domain and app token in the appropriate places.
    ```
    export gotify_enabled=true
    export gotify_domain=https://gotify.domain.com
    export gotify_app_token=put_your_token_here
    export gotify_priority=5
    ```

# IFTTT
IFTTT is a completely free alternative that can be configured to send notifications. It requires an account and the IFTTT app to be installed but is available for both [iOS](https://itunes.apple.com/app/apple-store/id660944635) and [Android](https://play.google.com/store/apps/details?id=com.ifttt.ifttt).

1. Connect the [Webhooks service](https://ifttt.com/maker_webhooks)
1. Create a new applet
    1. Choose "Webhooks" as the service
    1. Choose "Receive a web request" as the trigger
    1. Provide a unique **Event Name** to create the trigger and note this down
    1. Choose "Notifications" as the action service
    1. Choose "Send a notification from the IFTTT app" as the action
    1. Customize the message to be something like
        ```
        {{Value1}} {{Value2}} {{Value3}} ({{OccurredAt}})
        ```
        - `Value3` will not be used by `teslausb`
        - Feel free to modify this later to your liking.
    1. Name and save the applet. You can modify the name, event name, and message by clicking on the Gear icon.
1. Test the applet out by going back to the [Webhooks service](https://ifttt.com/maker_webhooks) page and clicking on "Documentation".
1. Note down the **key**.
1. Trigger the test by providing the event name and optional values 1-3.
1. If it's not working, you can try to run the curl command manually via your command line and it should return a more informative error message. You can also try to generate a new **key** by going to the [Webhooks settings](https://ifttt.com/services/maker_webhooks/settings) page, and clicking "Edit Connection".
1. You should receive a notification within a few seconds. :)
1. Run these commands, substituting your event name and key in the appropriate places.
    ```
    export ifttt_enabled=true
    export ifttt_event_name=put_your_event_name_here
    export ifttt_key=put_your_key_here
    ```

# AWS SNS
You can also choose to send notification through AWS SNS. You can create a free AWS account and the free tier enables you to receive notifications via SNS for free.

1. Create a free account at [AWS](https://aws.amazon.com/).
1. Create a user in IAM and give it the rights to SNS.
1. Create a new SNS topic.
1. Create the notification end point (email or other)
1. Run these commands, substituting your user key and app key in the appropriate places. Use of `"` is required for aws_sns_topic_arn.
    ```
    export sns_enabled=true
    export aws_region=us-east-1
    export aws_access_key_id=put_your_accesskeyid_here
    export aws_secret_key=put_your_secretkey_here
    export aws_sns_topic_arn=put_your_sns_topicarn_here
    ```

