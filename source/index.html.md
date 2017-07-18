---
title: Smartsettle API Docs

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

toc_footers:
  - <a href='https://go.smartsettle.com/'>Get an API Key</a>
  - <a href='https://go.smartsettle.com/'>Smartsettle</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the Smartsettle API! You can use our API to access Smartsettle API endpoints, which can get information on negotiations.

Our api follows the <a href='http://jsonapi.org/format/' target='_blank'>JSON API v1 Format</a>

> API responses will look like this:

```json
{
  "data": {
    "type": "negotiation",
    "id": "1",
    "attributes": {
      // ... this negotiation's attributes
    },
    "relationships": {
      // ... this negotiation's relationships
    }
  }
}
```

# Authentication

Smartsettle uses your API key and email to authenticate with the API.

Smartsettle expects for the API key and email to be included in all API requests to the server headers.

> To authorize, use this code:

```shell
# With shell, you can just pass the correct headers with each request
curl "api_endpoint_here"
  -H "X-User-Email: example@example.com" -H "X-User-Token: meowmeowmeow"
```

> Make sure to replace `meowmeowmeow` with your API key.

# Negotiations

```shell
# Example:
curl "https://go.smartsettle.com/api/negotiations?page=1&per_page=50&ordering=your_role&search=settlement"
```

Smartsettle provides an api endpoint to retreive, filter, and order Negotiations.

The Negotiations API endpoint supports the following parameters:

Parameter | Acceptable Values | Result | Default
---------- | ------- | ------- | -------
search | String | Negotiations with a name or description matching your String. | null
ordering | String - default ascending, prefix with `-` for descending - `id`, `name`, `your_role`, `other_party`, `party_waiting_on`, `session_number`, `status`, `last_update` | Orders the results based on the defined value | `last_update DESC`
page | Int | Paginates Negotiations | 1
facilitating | boolean | By default, only the negotiations you are a party in are returned by the API. By setting this to true, negotiations that you are facilitating but not a party in are returned | false
per_page | Int | Defines the amount of Negotiations per page | 20

## Negotiation

To retrieve a single negotiation... Coming soon
