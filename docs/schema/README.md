# Frakture Schema

A Frakture Warehouse holds many types of objects that have been mapped from various source systems into a normalized schema.
The most common object types in a Frakture Warehouse are:

- **Messages**: Emails, Ads, Surveys... Any form of data that presents information to a person, and their statistics 
- **Transactions**: Donations, Gifts, Pledges... Any form of data that represents a monetary transfer
- **People**: Constituents, Volunteers, Donors... Any form of data that represents a single person

Each type has a specific set of *Standard* fields that will be found on the primary tables for that type.
The standard fields/tables can be found below:

## Messages

Frakture Warehouse messages for a given system can be found in the a view named `<table_prefix><channel>_summary`. For instance,
the Facebook Ads for a bot with table_prefix "fb_biz_1t5" would be "fb_biz_1t5_ads_summary".

The standard message definition fields are:

| Field | Description |
| --- | --- |
| remote_id | The unique identifier of the message within the source system |
| publish_date | The date when the message was published - this can be the send date of an email, the first day an ad is displayed, etc |
| label | A shortened title for the message - this can be the subject of an email, the title of an ad, etc |

In addition to these fields that are captured from the source system, there are several appended by Frakture:

| Field | Description |
| --- | --- |
| message_id | The unique identifier of the message within Frakture |
| channel | A short word describing the type of message - "email", "ad", "form", etc |
| primary_source_code | A Frakture Bots best guess at the source code associated with this message. Can be overriden |

Individual Message Statistics are also pulled into the Warehouse and supplied alongside these definition fields.

The standard message stat fields are described below, along with the standard definition for each*:

| Field | Description |
| --- | --- |
| impressions | How many times this message was seen by a target |
| clicks | How many times a link from that message was clicked |
| interactions | |
| revenue | The system reported amount of money generated by this Message |

* Systems have different ways of calculating, tracking, and presenting these values. To see how each maps to the source system, check the documentation for that system.

In addition to these fields, Frakture appends the following [Attribution](/enrichment/attribution/) fields:

| Field | Description |
| --- | --- |
| attributed_transactions | The number of monetary transactions that Frakture has attributed to this message |
| attributed_revenue | The sum total of monetary transactions that Frakture has attributed to this message |

Specific Message schema definitions can be found [here](/schema/messages).

## Transactions

Monetary transactions for a given system can be found in a table named `<table_prefix>transaction`.

The standard fields collected for monetary transactions are:

| Field | Description |
| --- | --- |
| remote_transaction_id | The unique identifier for this transaction in the source system |
| ts | The timestamp when this transaction was processed, as reported by the source system |
| amount | The amount of money reported by the source system |
| source_code* | An identifier from the source system that identifies how a transaction entered the system |

 * Systems have different ways of representing source code information, and occasionally this is spread across multiple fields.