---
title: Connecting to Slack
subtitle: Using a Webhook to Connect ProGet to Slack
sequence: 100
keywords: proget, webhooks, slack
---

[Webhooks](/docs/proget/advanced/webhooks) let you connect two tools to notify users, trigger automated workflows, or audit certain events. ProGet's webhooks are highly customizable: seven different "methods" (like "Post" or "Delete") and six different "events" (like "Pulled" or "Promoted") give you a possible 156 different notification alerts. 

In this page, we show you how to connect ProGet to Slack and sample payload messages to copy/paste into your own webhook.

## Configuring a Slack Webhook {#slack data-title="Configuring a Slack/ProGet Webhook"}

To connect to Slack, start by following [this Slack tutorial](https://api.slack.com/messaging/webhooks) to create your incoming webhook application inside Slack. Slack now recommends this as the best way to add webhooks (instead of the previously recommended third-party app called Incoming Webhooks).

![](/resources/documentation/proget/SlackWebHooks.png){.screenshot}

Once you've created your Incoming Webhook application in Slack, you can optionally change the notification colors and the app's icon.

![](/resources/documentation/proget/SlackApp.png){.screenshot}

Note that to edit the webhook again, you must go to "Your Apps" inside Slack, rather than from the channel where the webhook posts.

Inside **ProGet**, go to the Manage Feed page, click the "Webhooks" tab, and click "create." Note that you can create a webhook at the feed or at global level.

![](/resources/documentation/proget/Slack-ProGet-WebHook.png){.screenshot}

The payload can be tedious to configure, so you can test it by copy/pasting this sample Slack payload we created:

```
{"text": "*feed:* $FeedName, *package:* $PackageId, *version:* $PackageVersion, *hash:* $PackageHash, *packageType:* $FeedType, *event:* $WebhookEvent, *user:* $UserName"}
```

After you've saved your webhook, take the configured action in ProGet, and your Slack should receive a notification from ProGet!

![](/resources/documentation/proget/SlackMessageEvolution.png){.screenshot}

## Additional Notes

You can create webhooks from the individual feed pages or by going to Settings > Webhooks > Create Webhook. Creating a global webhook requires selecting "(all feeds)," but for Docker feeds, you will not be able to select this due to different Docker URLs.

Webhooks are configurable in all versions of ProGet, but they will not fire in free editions.
