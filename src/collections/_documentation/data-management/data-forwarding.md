---
title: 'Data Forwarding'
sidebar_order: 3
---

Sentry provides the ability to forward processed events to certain third party providers such as [Segment](https://segment.com) and [Amazon SQS](https://aws.amazon.com/sqs/).

This is commonly useful in places where you may want to do deeper analysis on exceptions, or empower other teams, such as a Business Intelligence function.

Configuring Data Forwarding is done by visiting **[Project] » Settings » Data Forwarding** and filling in the required information for the given integration.

## Amazon SQS {#id1}

Integration with Amazon SQS makes it quick and easy to pipe exceptions back into your own systems.

The payload for Amazon is identical is our standard API event payload, and will evolve over time. For more details on the format of this data, see our [API documentation]({%- link _documentation/api/events/get-project-event-details.md -%}).

## Segment {#id2}

The Segment integration will generate _Error Captured_ events within your data pipeline. These events will **only** be captured for for `error` events, and only when an ID is present the user context. The general shape of the event will look roughly similar to:

```json
{
  "userId": "1",
  "event": "Error Captured",
  "properties": {
      "environment": "production",
      "eventId": "002c8bbde8324dae9f12a0b96f5b1e51",
      "exceptionType": "ValueError",
      "release": "a2def1",
      "transaction": "/api/0/users/{user}/",
      "userAgent": "Mozilla/5.0 (X11; Linux x86_64; rv:54.0) Gecko/20100101 Firefox/54.0",
      "page": {
        "url": "https://sentry.io/api/0/users/{user}/",
        "method": "GET",
        "search": "",
        "referer": "https://sentry.io/"
      }
  },
  "timestamp": "2017-05-20T15:29:06Z"
}
```

## Splunk

For details on the Splunk integration, visit the dedicated [_Splunk integration documentation_]({%- link _documentation/workflow/integrations/splunk.md -%}).