## Data Model And Approach

We will start with just the `browse` event for now. Eventually, we can add multiple events, such as: browse, click, share, purchase.

There are two ways to perform recommendations:
1. One endpoint to get weighted recommendations by the event,
2. Separate endpoints to get recommendations for each event type, and then handle the weights / combinations in the UI separately.

^ Which way to go here should be driven by the use-case. That said, both fundamentally use the same approach.

In v1, we will build out the PoC assuming there is a single event.

## Data Shape Assumptions

The index consists of documents that are events. The `url` key indicates the URL visited and the `event` key indicates the type of event. An example doc would look like:

{
    "_id": auto-generated,
    "user_id": "<some_string>",
    "url": "abc",
    "event": "browse",
    "timestamp": "2020-05-20"
}

Note: I want to start out by not doing any roll-ups at insertion time. Keep each document unique.

## How Data Generation Works -> Script to be done later

1. Have a dictionary of user ids
2. Have a dictionary of URLs
3. Generate one of the possible events
4. Generate one of the possible timestamps

## How The Recommendation Query Works


Query:

1. Provide a history or URLs with the specific event..
   1. Specify with a terms query
2. Apply the significant terms aggregation.
