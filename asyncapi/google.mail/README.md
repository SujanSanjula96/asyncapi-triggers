## Overview

The Gmail Ballerina Trigger supports to listen to the changes of Gmail mailbox such as receiving a new message, receiving a new thread, adding a new label to a message, adding star to a message, removing label from a message, removing star from a message, and receiving a new attachment with the following trigger methods: `onNewEmail`, `onNewThread`, `onEmailLabelAdded`, `onEmailStarred`, `onEmailLabelRemoved`,`onEmailStarRemoved`, `onNewAttachment`.

This module supports [Gmail API v1](https://developers.google.com/gmail/api).

## Prerequisites

Before using this connector in your Ballerina application, complete the following:

1. Create a [Google account](https://accounts.google.com/signup/v2/webcreateaccount?utm_source=ga-ob-search&utm_medium=google-account&flowName=GlifWebSignIn&flowEntry=SignUp). (If you already have one, you can use that.)

2. Obtain tokens

- Follow [this guide](https://developers.google.com/identity/protocols/oauth2)
  > **Note :** Enable `Cloud Pub/Sub API` or user setup service account with pubsub admin role. [Create a service account](https://developers.google.com/identity/protocols/oauth2/service-account#creatinganaccount) with pubsub admin

### Compatibility

|                    | Version                       |
| ------------------ |-------------------------------|
| Ballerina Language | Ballerina Swan Lake 2201.11.0 |

## Quickstart

To use the `Gmail` Trigger in your Ballerina application, update the .bal file as follows:

### Step 1: Import the Gmail Ballerina Trigger library

Import the ballerinax/trigger.google.mail module into the Ballerina project.

```ballerina
    import ballerinax/trigger.google.mail;
```

### Step 2: Initialize the Gmail Webhook Listener

Initialize the Trigger by providing the listener config & port number/httpListener object.

```ballerina
    mail:ListenerConfig config = {
        clientId: "xxxx",
        clientSecret: "xxxx",
        refreshUrl: "https://oauth2.googleapis.com/token",
        refreshToken: "xxxx",
        pushEndpoint: "xxxx",
        project: "xxxx"
    };
    listener mail:Listener webhookListener = new(config, 8090);
```

> **NOTE :**
>
> Here
>
> - `project` is the Id of the project which is created in `Google Cloud Platform` to create credentials (`clientId` and `clientSecret`).
> - `pushEndpoint` is the endpoint URL of the listener.

### Step 3: Use the correct service type to implement the service

Initialize the GmailService as below.

```ballerina
service mail:GmailService on webhookListener {

    remote function onEmailLabelAdded(mail:ChangedLabel changedLabel) returns error? {
        return;
    }

    remote function onEmailLabelRemoved(mail:ChangedLabel changedLabel) returns error? {
        return;
    }

    remote function onEmailStarRemoved(mail:Message message) returns error? {
        return;
    }

    remote function onEmailStarred(mail:Message message) returns error? {
        log:printInfo(message.toString());
        return;
    }

    remote function onNewAttachment(mail:MailAttachment attachment) returns error? {
        return;
    }

    remote function onNewEmail(mail:Message message) returns error? {
        return;
    }

    remote function onNewThread(mail:MailThread thread) returns error? {
        return;
    }
}
```

### Step 4: Provide remote functions corresponding to the events which you are interested on

The remote functions can be provided as follows.

```ballerina
    remote function onNewEmail(mail:Message message) returns error? {
        log:printInfo("Received new email", eventPayload = message);
    }
```

## Report issues

To report bugs, request new features, start new discussions, etc., go to the [Ballerina Library repository](https://github.com/ballerina-platform/ballerina-library)

## Useful links

- For more information go to the [`trigger.google.mail` package](https://central.ballerina.io/ballerinax/trigger.google.mail/latest).
- For example demonstrations of the usage, go to [Ballerina By Examples](https://ballerina.io/learn/by-example/).
- Chat live with us via our [Discord server](https://discord.gg/ballerinalang).
- Post all technical questions on Stack Overflow with the [#ballerina](https://stackoverflow.com/questions/tagged/ballerina) tag.
