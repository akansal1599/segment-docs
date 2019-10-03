---
title: 'Spec: Common Fields'
sidebar: Common Fields
---

In the Segment [Spec](/docs/spec/) all the [API calls](/docs/spec#api-calls) have a common structure, and a few common fields. However, not every destination accepts every specced field. If you have a question about what fields a destination *will* accept, you can refer to the destination's docs page, or check out our [open-source destination code on Github](https://github.com/segment-integrations).

## Structure
Every API call has the same core structure and fields. These fields describe user identity, timestamping and mechanical aides like API version.

Here's an example of these common fields in raw JSON:

```json
{
  "anonymousId": "507f191e810c19729de860ea",
  "context": {
    "active": true,
    "app": {
      "name": "InitechGlobal",
      "version": "545",
      "build": "3.0.1.545",
      "namespace": "com.production.segment"
    },
    "campaign": {
      "name": "TPS Innovation Newsletter",
      "source": "Newsletter",
      "medium": "email",
      "term": "tps reports",
      "content": "image link"
    },
    "device": {
      "id": "B5372DB0-C21E-11E4-8DFC-AA07A5B093DB",
      "advertisingId": "7A3CBEA0-BDF5-11E4-8DFC-AA07A5B093DB",
      "adTrackingEnabled": true,
      "manufacturer": "Apple",
      "model": "iPhone7,2",
      "name": "maguro",
      "type": "ios",
      "token": "ff15bc0c20c4aa6cd50854ff165fd265c838e5405bfeb9571066395b8c9da449"
    },
    "ip": "8.8.8.8",
    "library": {
      "name": "analytics.js",
      "version": "2.11.1"
    },
    "locale": "nl-NL",
    "location": {
      "city": "San Francisco",
      "country": "United States",
      "latitude": 40.2964197,
      "longitude": -76.9411617,
      "speed": 0
    },
    "network": {
      "bluetooth": false,
      "carrier": "T-Mobile NL",
      "cellular": true,
      "wifi": false
    },
    "os": {
      "name": "iPhone OS",
      "version": "8.1.3"
    },
    "page": {
      "path": "/academy/",
      "referrer": "",
      "search": "",
      "title": "Analytics Academy",
      "url": "https://segment.com/academy/"
    },
    "referrer": {
      "id": "ABCD582CDEFFFF01919",
      "type": "dataxu"
    },
    "screen": {
      "width": 320,
      "height": 568,
      "density": 2
    },
    "groupId": "12345",
    "timezone": "Europe/Amsterdam",
    "userAgent": "Mozilla/5.0 (iPhone; CPU iPhone OS 9_1 like Mac OS X) AppleWebKit/601.1.46 (KHTML, like Gecko) Version/9.0 Mobile/13B143 Safari/601.1"
  },
  "integrations": {
    "All": true,
    "Mixpanel": false,
    "Salesforce": false
  },
  "messageId": "022bb90c-bbac-11e4-8dfc-aa07a5b093db",
  "receivedAt": "2015-12-10T04:08:31.909Z",
  "sentAt": "2015-12-10T04:08:31.581Z",
  "timestamp": "2015-12-10T04:08:31.905Z",
  "type": "track",
  "userId": "97980cfea0067",
  "version": 2
}
```

In more detail these common fields for every API call are:
<table>
  <tr>
    <th>**Field**</th>
    <th>**Type**</th>
    <th>**Description**</th>
  </tr>
  {% include content/spec-field-anonymous-id.md %}
  {% include content/spec-field-context.md %}
  {% include content/spec-field-integrations.md %}
  {% include content/spec-field-message-id.md %}
  {% include content/spec-field-received-at.md %}
  {% include content/spec-field-sent-at.md %}
  {% include content/spec-field-timestamp.md %}
  {% include content/spec-field-type.md %}
  {% include content/spec-field-user-id.md %}
  {% include content/spec-field-version.md %}
</table>

Beyond this common structure, each API call adds a few specialized top-level fields.

## Context

Context is a dictionary of extra information that provides useful context about a datapoint, for example the user's `ip` address or `locale`. Context is a complete and explicit specification, so properties outside the spec will be ignored. You should **only use** Context fields for their intended meaning.

<table>
  <tr>
    <th>**Field**</th>
    <th>**Type**</th>
    <th>**Description**</th>
  </tr>
  <tr>
    <td>`active`</td>
    <td>Boolean</td>
    <td>Whether a user is active
      <p>This is usually used to flag an `.identify()` call to just update the traits but not "last seen."</p>
    </td>
  </tr>
  <tr>
    <td>`app` </td>
    <td>Object</td>
    <td>dictionary of information about the current application, containing `name`, `version` and `build`.
      <p>This is collected automatically from our mobile libraries when possible.</p>
    </td>
  </tr>
  <tr>
    <td>`campaign`</td>
    <td>Object</td>
    <td>Dictionary of information about the campaign that resulted in the API call, containing `name`, `source`, `medium`, `term` and `content`
      <p>This maps directly to the common UTM campaign parameters.</p>
    </td>
  </tr>
  <tr>
    <td>`device` </td>
    <td>Object</td>
    <td>Dictionary of information about the device, containing `id`, `manufacturer`, `model`, `name`, `type` and `version`</td>
  </tr>
  <tr>
    <td>`ip`</td>
    <td>String</td>
    <td>Current user's IP address</td>
  </tr>
  <tr>
    <td>`library` </td>
    <td>Object</td>
    <td>Dictionary of information about the library making the requests to the API, containing `name` and `version`</td>
  </tr>
  <tr>
    <td>`locale` </td>
    <td>String</td>
    <td>Locale string for the current user, for example `en-US`</td>
  </tr>
  <tr>
    <td>`location`</td>
    <td>Object</td>
    <td>Dictionary of information about the user's current location, containing `city`, `country`, `latitude`, `longitude`, `region` and `speed`</td>
  </tr>
  <tr>
    <td>`network`</td>
    <td>Object</td>
    <td>Dictionary of information about the current network connection, containing `bluetooth`, `carrier`, `cellular` and `wifi`</td>
  </tr>
  <tr>
    <td>`os`</td>
    <td>Object</td>
    <td>Dictionary of information about the operating system, containing `name` and `version`</td>
  </tr>
  <tr>
    <td>`page`</td>
    <td>Object</td>
    <td>Dictionary of information about the current page in the browser, containing `hash`, `path`, `referrer`, `search`, `title` and `url`
      <p>Automatically collected by Analytics.js.</p>
    </td>
  </tr>
  <tr>
    <td>`referrer`</td>
    <td>Object</td>
    <td>Dictionary of information about the way the user was referred to the website or app, containing `type`, `name`, `url` and `link`</td>
  </tr>
  <tr>
    <td>`screen`</td>
    <td>Object</td>
    <td>Dictionary of information about the device's screen, containing `density`, `height` and `width`</td>
  </tr>
  <tr>
    <td>`timezone`</td>
    <td>String</td>
    <td>Timezones are sent as tzdata strings to add user timezone information which might be stripped from the timestamp
      <p>Ex: `America/New_York`</p>
    </td>
  </tr>
  <tr>
    <td>`groupId`</td>
    <td>String</td>
    <td>Group / Account ID.
      <p>This is useful in B2B use cases where you need to attribute your non-group calls to a company or account. It is relied on by several Customer Success and CRM tools.</p></td>
  </tr>
  <tr>
    <td>`traits`</td>
    <td>Object</td>
    <td>Dictionary of `traits` of the current user
      <p>This is useful in cases where you need to `track` an event, but also associate information from a previous `identify` call. You should fill this object the same way you would fill traits in an [identify call](/docs/spec/identify/#traits).</p></td>
  </tr>
  <tr>
    <td>`userAgent`</td>
    <td>String</td>
    <td>User agent of the device making the request</td>
  </tr>
</table>

## Context Fields Automatically Collected

Below is a chart that shows you which context variables are populated automatically by our iOS, Android and analytics.js libraries.

Other libraries only collect `context.library`, any other context variables must be sent manually.

| Context Field            | Analytics.js | Analytics-ios | Analytics-android |
|--------------------------|--------------|---------------|-------------------|
| app.name                 |              |     √         |      √            |
| app.version              |              |     √         |      √            |
| app.build                |              |     √         |      √            |
| campaign.name            |     √        |               |                   |
| campaign.source          |     √        |               |                   |
| campaign.medium          |     √        |               |                   |
| campaign.term            |     √        |               |                   |
| campaign.content         |     √        |               |                   |
| device.type              |              |               |      √            |
| device.id                |              |     √         |      √            |
| device.advertisingId     |              |     √         |      √            |
| device.adTrackingEnabled |              |     √         |      √            |
| device.manufacturer      |              |     √         |      √            |
| device.model             |              |     √         |      √            |
| device.name              |              |               |      √            |
| library.name             |     √        |     √         |      √            |
| library.version          |     √        |     √         |      √            |
| ip*                      |     √        |     √         |      √            |
| locale                   |              |     √         |      √            |
| location.latitude        |              |               |                   |
| location.longitude       |              |               |                   |
| location.speed           |              |               |                   |
| network.bluetooth        |              |               |      √            |
| network.carrier          |              |     √         |      √            |
| network.cellular         |              |     √         |      √            |
| network.wifi             |              |     √         |      √            |
| os.name                  |              |     √         |      √            |
| os.version               |              |     √         |      √            |
| page.path                |      √       |               |                   |
| page.referrer            |      √       |               |                   |
| page.search              |      √       |               |                   |
| page.title               |      √       |               |                   |
| page.url                 |      √       |               |                   |
| screen.density           |              |               |      √            |
| screen.height            |              |      √        |      √            |
| screen.width             |              |      √        |      √            |
| traits                   |              |      √        |      √            |
| userAgent                |      √       |               |      √            |
| timezone                 |              |      √        |      √            |

* IP Address is not collected by our libraries, but instead filled in by our servers when it receives a message for **client side events only**.
* Our Android library collects `screen.density` with [this method](/docs/spec/common/#context-fields-automatically-collected).

## Integrations

A dictionary of destination names that the message should be sent to. `'All'` is a special key that applies when no key for a specific destination is found.

Integrations defaults to the following:

```
{
  All: true,
  Salesforce: false,
}
```

This is because [Salesforce](/docs/integrations/salesforce/) has strict limits on API calls, and we don't want to run over your limits by accident.

Sending data to the rest of our destinations is opt-out so if you don't specify the destination as false in this object, it will be sent to rest of the destinations that can accept it.


## Timestamps

Every API call has four timestamps, `originalTimestamp`, `timestamp`, `sentAt` and `receivedAt.`  They're used for very different purposes.

**All timestamps are [ISO-8601](http://en.wikipedia.org/wiki/ISO_8601) date strings.**

### Timestamp Overview

<table>
<col width="20%">
<col width="40%">
<col width="40%">
  <tr>
    <th>Timestamp</th>
    <th>Calculated</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>originalTimestamp</td>
    <td>
      <p>Time on the client device when call was invoked</p>
      <p>**OR**</p>
      <p>`timestamp` value manually passed in through server-side libraries</p>
    </td>
    <td>
      <p>Used by Segment to calculate `timestamp`</p>
      <p>**Note:** `originalTimestamp` is not useful for analysis since it's not always trustworthy as it can be easily adjusted and affected by clock skew</p>
    </td>
  </tr>
  <tr>
    <td>sentAt</td>
    <td>
      <p>Time on client device when call was sent</p>
      <p>**OR**</p>
     <p>`sentAt` value manually passed in</p>
    </td>
    <td>
      <p>Used by Segment to calculate `timestamp`</p>
      <p>**Note:** `sentAt` is not useful for analysis since it's not always trustworthy as it can be easily adjusted and affected by clock skew</p>
    </td>
  </tr>
  <tr>
    <td>receivedAt</td>
    <td>time on Segment server clock when call was received</td>
    <td>
      <p>Used by Segment to calculate `timestamp`</p>
      <p>Used as sort key in Warehouses</p>
      <p>**Note:** For max query speed, `receivedAt` is the recommended timestamp for analysis when chronology does not matter as chronology is not ensured</p>
    </td>
  </tr>
  <tr>
    <td>timestamp</td>
    <td>
      <p>Calculated by Segment to correct client-device clock skew using the following formula:</p>
      <p>`receivedAt` - (`sentAt` - `originalTimestamp`)</p>
    </td>
    <td>
      <p>Used by Segment to send to downstream destinations</p>
      <p>Used for historical replays</p>
      <p>**Note:** Recommended timestamp for analysis when chronology does matter</p>
    </td>
  </tr>
</table>


### `originalTimestamp`

The `originalTimestamp` tells you when call was invoked on the client device or the value of `timestamp` that you manually passed in.

**Note:** The `originalTimestamp` timestamp is not useful for any analysis since it's not always trustworthy as it can be easily adjusted and affected by clock skew.


### `sentAt`

The `sentAt` timestamp specifies the clock time for the client's device when the network request was made to the Segment API. For libraries and systems that send batched requests, there can be a long gap between a datapoint's `timestamp` and `sentAt`. Combined with `receivedAt`, we can use `sentAt` to correct the original `timestamp` in situations where a user's device clock cannot be trusted (mobile phones and browsers). The `sentAt` and `receivedAt` timestamps are assumed to occur at the same time (maximum a few hundred milliseconds), and therefore the difference is the user's device clock skew, which can be applied back to correct the `timestamp`.

**Note:** The `sentAt` timestamp is not useful for any analysis since it's tainted by user's clock skew.


### `receivedAt`

The `receivedAt` timestamp is added to incoming messages as soon as they hit our API. It's used in combination with `sentAt` to correct clock skew, and also to aid with debugging libraries and systems that deliver events in batches.

The `receivedAt` timestamp is most important as the sort key in our Warehouses product. Use this for max query speed when retrieving data from your Warehouse!

**Note:** Chronological order of events is not ensured with `receivedAt`.

### `timestamp`

The `timestamp` timestamp specifies when the datapoint occurred, corrected for client-device clock skew. This is the timestamp that is passed to downstream destinations and used for historical replays. It is important to use this timestamp for importing historical data to the API.

The `timestamp` field is settable from our server-side libs or if passing info directly to the HTTP endpoints.