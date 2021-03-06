# Flows

A flow in Flowdock is like one single team workspace, which contains a chat room and a shared inbox.

In the REST API, Flow IDs are of the form `:organization/:flow`.

* `organization` is the parametric name of the client organization, as seen in the subdomain of the web URL of the flow. 
* `flow` is the parametric name of the flow, as seen in the path of the web URL of the flow. Eg. `https://:organization.flowdock.com/flows/:flow`

## List Flows
Lists the flows that the authenticated user has access to.

```
GET /flows
```

### Parameters

* `users`: boolean value (1/0) controlling whether a list of users should be included in for each flow.

### Response
```
[
  {
    "id": "acme/my-flow",
    "name": "My flow",
    "organization": "Acme",
    "unread_mentions": 0,
    "url": "https://api.flowdock.com/flows/acme/my-flow",
    "web_url": "https://acme.flowdock.com/flows/my-flow"
  },
  {
    "id": "acme/another-flow",
    "name": "Another flow",
    "organization": "Acme",
    "unread_mentions": 0,
    "url": "https://api.flowdock.com/flows/acme/another-flow",
    "web_url": "https://acme.flowdock.com/flows/another-flow"
  },
]
```

* `id`: Flow resource ID
* `url`: Flow resource URL
* `web_url`: URL to the flow in the web UI
* `name`: Human-readable name of the flow
* `organization`: Human-readable name of the organization
* `unread_mentions`: Count of unread messages that mention the authenticated user


## Get a Flow
```
GET /flows/:organization/:flow
```
Get a single flow. Single flow information always includes user list of flow. Otherwise the data format is identical to the list. Timestamps are milliseconds since epoch.

### Response
```
{
  "id": "acme/my-flow",
  "name": "My flow",
  "organization": "Acme",
  "unread_mentions": 0,
  "url": "https://api.flowdock.com/flows/acme/my-flow",
  "web_url": "https://acme.flowdock.com/flows/my-flow",
  "users": [
    {
      "id": 9,
      "nick": "Joe",
      "name": "Joe Smith",
      "email": "joe@example.com",
      "status": "Testing API",
      "last_activity": 1328016726423000,
      "last_ping": 1328017690004000
    },
    {
      "id": 42,
      "nick": "Stevie",
      "name": "Stevie Johnson",
      "email": "stevie@example.com",
      "status": null,
      "last_activity": 1328016712345000,
      "last_ping": 1328017612345000
    }
  ]
}
```
