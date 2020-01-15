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

Welcome to the Smartsettle API v1! You can use our API to access your negotiations, parties, and more! In the future we will support the negotiation intake and creation process.

Some of our API follows the <a href='http://jsonapi.org/format/' target='_blank'>JSON API v1 Format</a>.

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

Smartsettle expects your API key and email to be included in all API requests to the server. You can include key key pair in the request headers or as url parameters.

> To authorize, use this code:

```shell
# With shell, you can need to pass the correct headers with each request
curl "api_endpoint_here"
  -H "X-User-Email: example@example.com" -H "X-User-Token: 123abc"
```

> Make sure to replace `123abc` with your API key.

# Negotiation

## List Negotiations

```shell
# Example:
curl --get "https://go.smartsettle.com/api/v1/negotiations?page=1&per_page=50&ordering=your_role&search=settlement"
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

## Retrieve a Negotiation

> Sample Call

```shell
curl --get "https://go.smartsettle.com/api/v1/negotiations/:negotiation_id"
```

> Sample Response

```json
{
  "negotiation": {
    "id": 285,
    "description": null,
    "creator_user_id": 1,
    "negotiation_template_id": 10,
    "current_session_number": 1,
    "current_agreement_framework": 283,
    "agreement_timestamp": null,
    "arbitration_enabled": null,
    "status": "active_sessions",
    "created_at": "2017-07-19T23:14:33.052Z",
    "updated_at": "2017-07-19T23:14:36.772Z",
    "creator_type": "party",
    "mode": "practice",
    "your_role": "JILL",
    "other_party": "GEORGE",
    "party_waiting_on": "You",
    "last_update": "19 Jul 23:14",
    "status_msg": "Active negotiation",
    "other_party_availibility": "offline",
    "url": "http://localhost:3000/negotiations/285",
    "name": "Collaborative George & Jill Spousal Support",
    "final_session": false,
    "all_accepted_framework": false
  }
}
```

Retrieve information about specific negotiation. All you need to know is the negotiation id.

## Update Acceptance

> Sample Call

```shell
curl --get "https://go.smartsettle.com/api/v1/negotiations/:negotiation_id/update_acceptance"
```

> Sample Response

```json
{
  "issue_id": "298",
  "acceptance": 100,
  "issue_slider_details": {
    "negotiation_id": 285,
    "negotiation_status": "active_sessions",
    "current_session": 1,
    "your_party_id": 556,
    "your_party_status": "active",
    "your_party_issue_preference_set": true,
    "other_party_id": 557,
    "other_party_status": "active",
    "other_party_issue_preference_set": true,
    "issue_id": 298,
    "issue_name": "Amount of spousal support to be paid",
    "issue_description": "Amount of spousal support to pay",
    "issue_formatted_description": "Amount of spousal support to pay (CAD)",
    "has_proposed": false,
    "has_accepted": true,
    "other_party_has_proposed": false,
    "other_party_has_accepted": false,
    "your_party_issue_preference": "higher",
    "preferred_value": 900,
    "unpreferred_value": 500,
    "grid_increment": 10,
    "visible_proposal": 900,
    "acceptance": 900,
    "initial_proposal": 900,
    "walkaway": 500,
    "counter_proposal": 500,
    "counter_initial_proposal": 500,
    "has_set_initial_proposal": false,
    "has_walkaway": "no",
    "other_party_issue_preference": "lower",
    "suggestion_set": [
      500,
      510,
      520,
      530,
      540,
      550,
      560,
      570,
      580,
      590,
      600,
      610,
      620,
      630,
      640,
      650,
      660,
      670,
      680,
      690,
      700,
      710,
      720,
      730,
      740,
      750,
      760,
      770,
      780,
      790,
      800,
      810,
      820,
      830,
      840,
      850,
      860,
      870,
      880,
      890,
      900
    ],
    "session_data": [
      100
    ],
    "acceptance_on_grid": true,
    "proposal_on_grid": true
  },
  "negotiation": {
    "id": 285,
    "status": "active_sessions",
    "current_session_number": 1,
    "negotiation_status": "Session 1 - waiting for you to make an initial proposal",
    "arbitration_enabled": true,
    "show_guided_help": true,
    "your_party": {
      "id": 556,
      "name": "Derek Barber",
      "role": "Party A",
      "status": "active",
      "arbitration_accepted": false,
      "af_status": "accepted",
      "can_end_session": false,
      "has_ended_session": "no",
      "has_declared_done": "no",
      "has_accepted": "yes",
      "has_proposed": "no"
    },
    "other_party": {
      "id": 557,
      "name": "George",
      "role": "Party B",
      "status": "active",
      "arbitration_accepted": false,
      "af_status": "unaccepted",
      "has_ended_session": "no",
      "has_declared_done": "no",
      "has_accepted": "no",
      "has_proposed": "no"
    },
    "session": {
      "final_session": "no"
    },
    "af": {
      "is_configured": "yes",
      "status": "ready",
      "party_lock_id": 0
    },
    "slider_grids_params": {
      "issue_298": {
        "negotiation_id": 285,
        "negotiation_status": "active_sessions",
        "current_session": 1,
        "your_party_id": 556,
        "your_party_status": "active",
        "your_party_issue_preference_set": true,
        "other_party_id": 557,
        "other_party_status": "active",
        "other_party_issue_preference_set": true,
        "issue_id": 298,
        "issue_name": "Amount of spousal support to be paid",
        "issue_description": "Amount of spousal support to pay",
        "issue_formatted_description": "Amount of spousal support to pay (CAD)",
        "has_proposed": false,
        "has_accepted": true,
        "other_party_has_proposed": false,
        "other_party_has_accepted": false,
        "your_party_issue_preference": "higher",
        "preferred_value": 900,
        "unpreferred_value": 500,
        "grid_increment": 10,
        "visible_proposal": 900,
        "acceptance": 900,
        "initial_proposal": 900,
        "walkaway": 500,
        "counter_proposal": 500,
        "counter_initial_proposal": 500,
        "has_set_initial_proposal": false,
        "has_walkaway": "no",
        "other_party_issue_preference": "lower",
        "suggestion_set": [
          500,
          510,
          520,
          530,
          540,
          550,
          560,
          570,
          580,
          590,
          600,
          610,
          620,
          630,
          640,
          650,
          660,
          670,
          680,
          690,
          700,
          710,
          720,
          730,
          740,
          750,
          760,
          770,
          780,
          790,
          800,
          810,
          820,
          830,
          840,
          850,
          860,
          870,
          880,
          890,
          900
        ],
        "session_data": [
          100
        ],
        "acceptance_on_grid": true,
        "proposal_on_grid": true
      }
    }
  },
  "success": true,
  "message": "Acceptance has been updated"
}
```

Update the current parties acceptance value for the current negotiation session.

Parameter | Acceptable Values  | Required
---------- | -------  | -------
issue_id | Integer | yes
acceptance | Integer | yes


## Update Visible Proposal

> Sample Call

```shell
curl --get "https://go.smartsettle.com/api/v1/negotiations/:negotiation_id/update_visible_proposal"
```

> Sample Response

```json
{
  "issue_id": "298",
  "visible_proposal": 840,
  "issue_slider_details": {
    "negotiation_id": 285,
    "negotiation_status": "active_sessions",
    "current_session": 1,
    "your_party_id": 556,
    "your_party_status": "active",
    "your_party_issue_preference_set": true,
    "other_party_id": 557,
    "other_party_status": "active",
    "other_party_issue_preference_set": true,
    "issue_id": 298,
    "issue_name": "Amount of spousal support to be paid",
    "issue_description": "Amount of spousal support to pay",
    "issue_formatted_description": "Amount of spousal support to pay (CAD)",
    "has_proposed": true,
    "has_accepted": true,
    "other_party_has_proposed": false,
    "other_party_has_accepted": false,
    "your_party_issue_preference": "higher",
    "preferred_value": 900,
    "unpreferred_value": 500,
    "grid_increment": 10,
    "visible_proposal": 840,
    "acceptance": 840,
    "initial_proposal": 840,
    "has_set_initial_proposal": true,
    "has_walkaway": "no",
    "other_party_issue_preference": "lower",
    "suggestion_set": [
      500,
      510,
      520,
      530,
      540,
      550,
      560,
      570,
      580,
      590,
      600,
      610,
      620,
      630,
      640,
      650,
      660,
      670,
      680,
      690,
      700,
      710,
      720,
      730,
      740,
      750,
      760,
      770,
      780,
      790,
      800,
      810,
      820,
      830,
      840,
      850,
      860,
      870,
      880,
      890,
      900
    ],
    "session_data": [
      840
    ],
    "acceptance_on_grid": true,
    "proposal_on_grid": true
  },
  "negotiation": {
    "id": 285,
    "status": "active_sessions",
    "current_session_number": 1,
    "negotiation_status": "Session 1 - waiting for George's proposal.",
    "arbitration_enabled": true,
    "show_guided_help": true,
    "your_party": {
      "id": 556,
      "name": "Derek Barber",
      "role": "Party A",
      "status": "active",
      "arbitration_accepted": false,
      "af_status": "accepted",
      "can_end_session": true,
      "has_ended_session": "no",
      "has_declared_done": "no",
      "has_accepted": "yes",
      "has_proposed": "yes"
    },
    "other_party": {
      "id": 557,
      "name": "George",
      "role": "Party B",
      "status": "active",
      "arbitration_accepted": false,
      "af_status": "unaccepted",
      "has_ended_session": "no",
      "has_declared_done": "no",
      "has_accepted": "no",
      "has_proposed": "no"
    },
    "session": {
      "final_session": "no"
    },
    "af": {
      "is_configured": "yes",
      "status": "ready",
      "party_lock_id": 0
    },
    "slider_grids_params": {
      "issue_298": {
        "negotiation_id": 285,
        "negotiation_status": "active_sessions",
        "current_session": 1,
        "your_party_id": 556,
        "your_party_status": "active",
        "your_party_issue_preference_set": true,
        "other_party_id": 557,
        "other_party_status": "active",
        "other_party_issue_preference_set": true,
        "issue_id": 298,
        "issue_name": "Amount of spousal support to be paid",
        "issue_description": "Amount of spousal support to pay",
        "issue_formatted_description": "Amount of spousal support to pay (CAD)",
        "has_proposed": true,
        "has_accepted": true,
        "other_party_has_proposed": false,
        "other_party_has_accepted": false,
        "your_party_issue_preference": "higher",
        "preferred_value": 900,
        "unpreferred_value": 500,
        "grid_increment": 10,
        "visible_proposal": 840,
        "acceptance": 840,
        "initial_proposal": 840,
        "has_set_initial_proposal": true,
        "has_walkaway": "no",
        "other_party_issue_preference": "lower",
        "suggestion_set": [
          500,
          510,
          520,
          530,
          540,
          550,
          560,
          570,
          580,
          590,
          600,
          610,
          620,
          630,
          640,
          650,
          660,
          670,
          680,
          690,
          700,
          710,
          720,
          730,
          740,
          750,
          760,
          770,
          780,
          790,
          800,
          810,
          820,
          830,
          840,
          850,
          860,
          870,
          880,
          890,
          900
        ],
        "session_data": [
          840
        ],
        "acceptance_on_grid": true,
        "proposal_on_grid": true
      }
    }
  },
  "success": true,
  "message": "Visible Proposal has been updated"
}
```
Update the visible proposal for a specific issue.

Parameter | Acceptable Values  | Required
---------- | -------  | -------
issue_id | Integer | yes
visible_proposal | Integer | yes

## Update Acceptance & Visible Proposal

> Sample Call

```shell
curl --get "https://go.smartsettle.com/api/v1/negotiations/:negotiation_id/update_acceptance_and_visible_proposal"
```

> Sample Response

```json
{
  "issue_id": "298",
  "visible_proposal": 840,
  "issue_slider_details": {
    "negotiation_id": 285,
    "negotiation_status": "active_sessions",
    "current_session": 1,
    "your_party_id": 556,
    "your_party_status": "active",
    "your_party_issue_preference_set": true,
    "other_party_id": 557,
    "other_party_status": "active",
    "other_party_issue_preference_set": true,
    "issue_id": 298,
    "issue_name": "Amount of spousal support to be paid",
    "issue_description": "Amount of spousal support to pay",
    "issue_formatted_description": "Amount of spousal support to pay (CAD)",
    "has_proposed": true,
    "has_accepted": true,
    "other_party_has_proposed": false,
    "other_party_has_accepted": false,
    "your_party_issue_preference": "higher",
    "preferred_value": 900,
    "unpreferred_value": 500,
    "grid_increment": 10,
    "visible_proposal": 840,
    "acceptance": 840,
    "initial_proposal": 840,
    "has_set_initial_proposal": true,
    "has_walkaway": "no",
    "other_party_issue_preference": "lower",
    "suggestion_set": [
      500,
      510,
      520,
      530,
      540,
      550,
      560,
      570,
      580,
      590,
      600,
      610,
      620,
      630,
      640,
      650,
      660,
      670,
      680,
      690,
      700,
      710,
      720,
      730,
      740,
      750,
      760,
      770,
      780,
      790,
      800,
      810,
      820,
      830,
      840,
      850,
      860,
      870,
      880,
      890,
      900
    ],
    "session_data": [
      840
    ],
    "acceptance_on_grid": true,
    "proposal_on_grid": true
  },
  "negotiation": {
    "id": 285,
    "status": "active_sessions",
    "current_session_number": 1,
    "negotiation_status": "Session 1 - waiting for George's proposal.",
    "arbitration_enabled": true,
    "show_guided_help": true,
    "your_party": {
      "id": 556,
      "name": "Derek Barber",
      "role": "Party A",
      "status": "active",
      "arbitration_accepted": false,
      "af_status": "accepted",
      "can_end_session": true,
      "has_ended_session": "no",
      "has_declared_done": "no",
      "has_accepted": "yes",
      "has_proposed": "yes"
    },
    "other_party": {
      "id": 557,
      "name": "George",
      "role": "Party B",
      "status": "active",
      "arbitration_accepted": false,
      "af_status": "unaccepted",
      "has_ended_session": "no",
      "has_declared_done": "no",
      "has_accepted": "no",
      "has_proposed": "no"
    },
    "session": {
      "final_session": "no"
    },
    "af": {
      "is_configured": "yes",
      "status": "ready",
      "party_lock_id": 0
    },
    "slider_grids_params": {
      "issue_298": {
        "negotiation_id": 285,
        "negotiation_status": "active_sessions",
        "current_session": 1,
        "your_party_id": 556,
        "your_party_status": "active",
        "your_party_issue_preference_set": true,
        "other_party_id": 557,
        "other_party_status": "active",
        "other_party_issue_preference_set": true,
        "issue_id": 298,
        "issue_name": "Amount of spousal support to be paid",
        "issue_description": "Amount of spousal support to pay",
        "issue_formatted_description": "Amount of spousal support to pay (CAD)",
        "has_proposed": true,
        "has_accepted": true,
        "other_party_has_proposed": false,
        "other_party_has_accepted": false,
        "your_party_issue_preference": "higher",
        "preferred_value": 900,
        "unpreferred_value": 500,
        "grid_increment": 10,
        "visible_proposal": 840,
        "acceptance": 840,
        "initial_proposal": 840,
        "has_set_initial_proposal": true,
        "has_walkaway": "no",
        "other_party_issue_preference": "lower",
        "suggestion_set": [
          500,
          510,
          520,
          530,
          540,
          550,
          560,
          570,
          580,
          590,
          600,
          610,
          620,
          630,
          640,
          650,
          660,
          670,
          680,
          690,
          700,
          710,
          720,
          730,
          740,
          750,
          760,
          770,
          780,
          790,
          800,
          810,
          820,
          830,
          840,
          850,
          860,
          870,
          880,
          890,
          900
        ],
        "session_data": [
          840
        ],
        "acceptance_on_grid": true,
        "proposal_on_grid": true
      }
    }
  },
  "success": true,
  "message": "Visible Proposal & Acceptance have been updated"
}
```

Update the visible proposal and acceptance to the same value for a specific issue.

Parameter | Acceptable Values  | Required
---------- | -------  | -------
issue_id | Integer | yes
visible_proposal | Integer | yes

## End Session

> Sample Call

```shell
curl --get "https://go.smartsettle.com/api/v1/negotiations/:negotiation_id/end_session"
```

> Sample Response

```json
{
  "negotiation": {
    "id": 285,
    "status": "active_sessions",
    "current_session_number": 1,
    "negotiation_status": "Session 1 - waiting for George's proposal.",
    "arbitration_enabled": true,
    "show_guided_help": true,
    "your_party": {
      "id": 556,
      "name": "Derek Barber",
      "role": "Party A",
      "status": "active",
      "arbitration_accepted": false,
      "af_status": "accepted",
      "can_end_session": false,
      "has_ended_session": "yes",
      "has_declared_done": "no",
      "has_accepted": "yes",
      "has_proposed": "yes"
    },
    "other_party": {
      "id": 557,
      "name": "George",
      "role": "Party B",
      "status": "active",
      "arbitration_accepted": false,
      "af_status": "unaccepted",
      "has_ended_session": "no",
      "has_declared_done": "no",
      "has_accepted": "no",
      "has_proposed": "no"
    },
    "session": {
      "final_session": "no"
    },
    "af": {
      "is_configured": "yes",
      "status": "ready",
      "party_lock_id": 0
    },
    "slider_grids_params": {
      "issue_298": {
        "negotiation_id": 285,
        "negotiation_status": "active_sessions",
        "current_session": 1,
        "your_party_id": 556,
        "your_party_status": "active",
        "your_party_issue_preference_set": true,
        "other_party_id": 557,
        "other_party_status": "active",
        "other_party_issue_preference_set": true,
        "issue_id": 298,
        "issue_name": "Amount of spousal support to be paid",
        "issue_description": "Amount of spousal support to pay",
        "issue_formatted_description": "Amount of spousal support to pay (CAD)",
        "has_proposed": true,
        "has_accepted": true,
        "other_party_has_proposed": false,
        "other_party_has_accepted": false,
        "your_party_issue_preference": "higher",
        "preferred_value": 900,
        "unpreferred_value": 500,
        "grid_increment": 10,
        "visible_proposal": 840,
        "acceptance": 840,
        "initial_proposal": 840,
        "has_set_initial_proposal": true,
        "has_walkaway": "no",
        "other_party_issue_preference": "lower",
        "suggestion_set": [
          500,
          510,
          520,
          530,
          540,
          550,
          560,
          570,
          580,
          590,
          600,
          610,
          620,
          630,
          640,
          650,
          660,
          670,
          680,
          690,
          700,
          710,
          720,
          730,
          740,
          750,
          760,
          770,
          780,
          790,
          800,
          810,
          820,
          830,
          840,
          850,
          860,
          870,
          880,
          890,
          900
        ],
        "session_data": [
          840
        ],
        "acceptance_on_grid": true,
        "proposal_on_grid": true
      }
    }
  },
  "success": true
}
```

End the session for this negotiation and the currently authenticated party.

## Declare Final Session

> Sample Call

```shell
curl --get "https://go.smartsettle.com/api/v1/negotiations/:negotiation_id/declare_final_session"
```

> Sample Response

```json
{
  "negotiation": {
    "id": 285,
    "status": "active_sessions",
    "current_session_number": 1,
    "negotiation_status": "Session 1 <b>(FINAL)</b> - Make final move and click \"Declare Done\"",
    "arbitration_enabled": true,
    "show_guided_help": true,
    "your_party": {
      "id": 556,
      "name": "Derek Barber",
      "role": "Party A",
      "status": "active",
      "arbitration_accepted": false,
      "af_status": "accepted",
      "can_end_session": false,
      "has_ended_session": "yes",
      "has_declared_done": "no",
      "has_accepted": "yes",
      "has_proposed": "yes"
    },
    "other_party": {
      "id": 557,
      "name": "George",
      "role": "Party B",
      "status": "active",
      "arbitration_accepted": false,
      "af_status": "unaccepted",
      "has_ended_session": "no",
      "has_declared_done": "no",
      "has_accepted": "no",
      "has_proposed": "no"
    },
    "session": {
      "final_session": "yes"
    },
    "af": {
      "is_configured": "yes",
      "status": "ready",
      "party_lock_id": 0
    },
    "slider_grids_params": {
      "issue_298": {
        "negotiation_id": 285,
        "negotiation_status": "active_sessions",
        "current_session": 1,
        "your_party_id": 556,
        "your_party_status": "active",
        "your_party_issue_preference_set": true,
        "other_party_id": 557,
        "other_party_status": "active",
        "other_party_issue_preference_set": true,
        "issue_id": 298,
        "issue_name": "Amount of spousal support to be paid",
        "issue_description": "Amount of spousal support to pay",
        "issue_formatted_description": "Amount of spousal support to pay (CAD)",
        "has_proposed": true,
        "has_accepted": true,
        "other_party_has_proposed": false,
        "other_party_has_accepted": false,
        "your_party_issue_preference": "higher",
        "preferred_value": 900,
        "unpreferred_value": 500,
        "grid_increment": 10,
        "visible_proposal": 840,
        "acceptance": 840,
        "initial_proposal": 840,
        "has_set_initial_proposal": true,
        "has_walkaway": "no",
        "other_party_issue_preference": "lower",
        "suggestion_set": [
          500,
          510,
          520,
          530,
          540,
          550,
          560,
          570,
          580,
          590,
          600,
          610,
          620,
          630,
          640,
          650,
          660,
          670,
          680,
          690,
          700,
          710,
          720,
          730,
          740,
          750,
          760,
          770,
          780,
          790,
          800,
          810,
          820,
          830,
          840,
          850,
          860,
          870,
          880,
          890,
          900
        ],
        "session_data": [
          840
        ],
        "acceptance_on_grid": true,
        "proposal_on_grid": true
      }
    }
  },
  "success": true
}
```

Declare final session for this negotiation as the currently authenticated party.

Parameter | Acceptable Values  | Required
---------- | -------  | -------
arbitration_accepted | Integer | optional

## Declare All Done

> Sample Call

```shell
curl --get "https://go.smartsettle.com/api/v1/negotiations/:negotiation_id/declare_all_done"
```

> Sample Response

```json
{
  "negotiation": {
    "id": 285,
    "status": "active_sessions",
    "current_session_number": 1,
    "negotiation_status": "Session 1 <b>(FINAL)</b> - Waiting for George",
    "arbitration_enabled": true,
    "show_guided_help": true,
    "your_party": {
      "id": 556,
      "name": "Derek Barber",
      "role": "Party A",
      "status": "active",
      "arbitration_accepted": false,
      "af_status": "accepted",
      "can_end_session": false,
      "has_ended_session": "yes",
      "has_declared_done": "yes",
      "has_accepted": "yes",
      "has_proposed": "yes"
    },
    "other_party": {
      "id": 557,
      "name": "George",
      "role": "Party B",
      "status": "active",
      "arbitration_accepted": false,
      "af_status": "unaccepted",
      "has_ended_session": "no",
      "has_declared_done": "no",
      "has_accepted": "no",
      "has_proposed": "no"
    },
    "session": {
      "final_session": "yes"
    },
    "af": {
      "is_configured": "yes",
      "status": "ready",
      "party_lock_id": 0
    },
    "slider_grids_params": {
      "issue_298": {
        "negotiation_id": 285,
        "negotiation_status": "active_sessions",
        "current_session": 1,
        "your_party_id": 556,
        "your_party_status": "active",
        "your_party_issue_preference_set": true,
        "other_party_id": 557,
        "other_party_status": "active",
        "other_party_issue_preference_set": true,
        "issue_id": 298,
        "issue_name": "Amount of spousal support to be paid",
        "issue_description": "Amount of spousal support to pay",
        "issue_formatted_description": "Amount of spousal support to pay (CAD)",
        "has_proposed": true,
        "has_accepted": true,
        "other_party_has_proposed": false,
        "other_party_has_accepted": false,
        "your_party_issue_preference": "higher",
        "preferred_value": 900,
        "unpreferred_value": 500,
        "grid_increment": 10,
        "visible_proposal": 840,
        "acceptance": 840,
        "initial_proposal": 840,
        "has_set_initial_proposal": true,
        "has_walkaway": "no",
        "other_party_issue_preference": "lower",
        "suggestion_set": [
          500,
          510,
          520,
          530,
          540,
          550,
          560,
          570,
          580,
          590,
          600,
          610,
          620,
          630,
          640,
          650,
          660,
          670,
          680,
          690,
          700,
          710,
          720,
          730,
          740,
          750,
          760,
          770,
          780,
          790,
          800,
          810,
          820,
          830,
          840,
          850,
          860,
          870,
          880,
          890,
          900
        ],
        "session_data": [
          840
        ],
        "acceptance_on_grid": true,
        "proposal_on_grid": true
      }
    }
  },
  "success": true
}
```

Declare all done for this negotiation and the currently authenticated party. All done means the party has locked in their final offers during the final session.

Parameter | Acceptable Values  | Required
---------- | -------  | -------
arbitration_accepted | Integer | optional

## Party Ping

> Sample Call

```shell
curl --get "https://go.smartsettle.com/api/v1/negotiations/:negotiation_id/party_ping"
```

> Sample Response

```json
{
  "success": true
}
```

Calling this endpoint will update the parties online status. This endpoint should be hit every 5 minutes if possible to allow us to maintain the online/offline status.

## Negotiation Status

> Sample Call

```shell
curl --get "https://go.smartsettle.com/api/v1/negotiations/:negotiation_id/negotiation_status"
```

> Sample Response

```json
{
  "negotiation": {
    "id": 285,
    "status": "active_sessions",
    "current_session_number": 1,
    "negotiation_status": "Session 1 - waiting for you to make an initial proposal",
    "arbitration_enabled": true,
    "show_guided_help": true,
    "your_party": {
      "id": 556,
      "name": "Jim",
      "role": "Party A",
      "status": "active",
      "arbitration_accepted": false,
      "af_status": "accepted",
      "can_end_session": false,
      "has_ended_session": "no",
      "has_declared_done": "no",
      "has_accepted": "no",
      "has_proposed": "no"
    },
    "other_party": {
      "id": 557,
      "name": "George",
      "role": "Party B",
      "status": "active",
      "arbitration_accepted": false,
      "af_status": "unaccepted",
      "has_ended_session": "no",
      "has_declared_done": "no",
      "has_accepted": "no",
      "has_proposed": "no"
    },
    "session": {
      "final_session": "no"
    },
    "af": {
      "is_configured": "yes",
      "status": "ready",
      "party_lock_id": 0
    },
    "slider_grids_params": {
      "issue_298": {
        "negotiation_id": 285,
        "negotiation_status": "active_sessions",
        "current_session": 1,
        "your_party_id": 556,
        "your_party_status": "active",
        "your_party_issue_preference_set": true,
        "other_party_id": 557,
        "other_party_status": "active",
        "other_party_issue_preference_set": true,
        "issue_id": 298,
        "issue_name": "Amount of spousal support to be paid",
        "issue_description": "Amount of spousal support to pay",
        "issue_formatted_description": "Amount of spousal support to pay (CAD)",
        "has_proposed": false,
        "has_accepted": false,
        "other_party_has_proposed": false,
        "other_party_has_accepted": false,
        "your_party_issue_preference": "higher",
        "preferred_value": 900,
        "unpreferred_value": 500,
        "grid_increment": 10,
        "visible_proposal": 900,
        "acceptance": 900,
        "initial_proposal": 900,
        "walkaway": 500,
        "counter_proposal": 500,
        "counter_initial_proposal": 500,
        "has_set_initial_proposal": false,
        "has_walkaway": "no",
        "other_party_issue_preference": "lower",
        "suggestion_set": [
          500,
          510,
          520,
          530,
          540,
          550,
          560,
          570,
          580,
          590,
          600,
          610,
          620,
          630,
          640,
          650,
          660,
          670,
          680,
          690,
          700,
          710,
          720,
          730,
          740,
          750,
          760,
          770,
          780,
          790,
          800,
          810,
          820,
          830,
          840,
          850,
          860,
          870,
          880,
          890,
          900
        ],
        "session_data": [

        ],
        "acceptance_on_grid": true,
        "proposal_on_grid": true
      }
    }
  },
  "success": true
}
```

Retrieve general information about specific negotiation. All you need to know is the negotiation id. This endpoint is intended to provide support for all the data required to render the negotiaion panel.

# Party

## Get Party

## Update Party

# User

## Get User

## Update User

## Create User

# History

## Get all entires

> Sample Call

```shell
curl --get "https://go.smartsettle.com/api/v1/history/:negotiation_id"
```

> Sample Response

```json
[
  {
    "id": 12573,
    "entry_type": "visible_concession",
    "body": "GEORGE made an initial proposal of 500",
    "negotiation_id": 285,
    "logged_at": "25 Jul 22:13",
    "time_ago": "2 minutes",
    "party_colour": "78BEF0"
  },
  {
    "id": 12574,
    "entry_type": "secret_acceptance",
    "body": "GEORGE updated their secret acceptance",
    "negotiation_id": 285,
    "logged_at": "25 Jul 22:13",
    "time_ago": "2 minutes",
    "party_colour": "78BEF0"
  },
  {
    "id": 12576,
    "entry_type": "accepted_framework",
    "body": "GEORGE accepted the Framework",
    "negotiation_id": 285,
    "logged_at": "25 Jul 22:13",
    "time_ago": "2 minutes",
    "party_colour": "78BEF0"
  },
  {
    "id": 12563,
    "entry_type": "final_session",
    "body": "Final session has been declared",
    "negotiation_id": 285,
    "logged_at": "25 Jul 21:56",
    "time_ago": "19 minutes",
    "party_colour": null
  },
  {
    "id": 12559,
    "entry_type": "secret_acceptance",
    "body": "JILL updated their secret acceptance from 100 to 840",
    "negotiation_id": 285,
    "logged_at": "25 Jul 21:39",
    "time_ago": "36 minutes",
    "party_colour": "BF607C"
  },
  {
    "id": 12556,
    "entry_type": "visible_concession",
    "body": "JILL made an initial proposal of 840",
    "negotiation_id": 285,
    "logged_at": "25 Jul 21:39",
    "time_ago": "36 minutes",
    "party_colour": "BF607C"
  },
  {
    "id": 12557,
    "entry_type": "secret_acceptance",
    "body": "JILL updated their secret acceptance from 900 to 100",
    "negotiation_id": 285,
    "logged_at": "20 Jul 22:40",
    "time_ago": "5 days",
    "party_colour": "BF607C"
  },
  {
    "id": 12564,
    "entry_type": "accepted_framework",
    "body": "JILL accepted the Framework",
    "negotiation_id": 285,
    "logged_at": "19 Jul 23:14",
    "time_ago": "6 days",
    "party_colour": "BF607C"
  },
  {
    "id": 12562,
    "entry_type": "framework_updated",
    "body": "JILL updated the Framework",
    "negotiation_id": 285,
    "logged_at": "19 Jul 23:14",
    "time_ago": "6 days",
    "party_colour": "BF607C"
  },
  {
    "id": 12561,
    "entry_type": "framework_updated",
    "body": "JILL updated the Framework",
    "negotiation_id": 285,
    "logged_at": "19 Jul 23:14",
    "time_ago": "6 days",
    "party_colour": "BF607C"
  },
  {
    "id": 12555,
    "entry_type": "negotiation_created",
    "body": "Negotiation was created",
    "negotiation_id": 285,
    "logged_at": "19 Jul 23:14",
    "time_ago": "6 days",
    "party_colour": null
  }
]
```

Retrieve the history logs for a given negotiation and context of the currently authenticated party. All you need to know is the negotiation id.

# Automated Negotiation Actions

You can pre schedule moves for each session and issue.

Requires documentation.

# Private Reference Packages

Lets you create a series of packages based on multiple issues. Currently it is used to create acceptable payment plans and used to derive an acceptable present value.

Requires documentation.

# Expert Neutral Negotiation

## List Expert Neutral Negotiations
Use the List Negotiations API endpoint in order retreive the availible cases that are pending END or have completed the END process. Passing account_role_id='expert_neutral' as a parameter will automatically filter negotiations appropriately for use as an END case list.

# Expert Neutral Values

## Update Expert Neutral Values

Parameter | Acceptable Values | Result | Default
---------- | ------- | ------- | -------
expert_neutral_value | String (required) | The value the EN chooses as their opionion | null

> Sample Call

```shell
curl --patch "https://go.smartsettle.com/api/v1/negotiations/:negotiation_id/expert_neutral_values/:issue_id?expert_neutral_value=450
```

## Destroy Expert Neutral Values

> Sample Call

```shell
curl --delete "https://go.smartsettle.com/api/v1/negotiations/:negotiation_id/expert_neutral_values/:issue_id"
```

## Show Expert Neutral Values

> Sample Call

```shell
curl --get "https://go.smartsettle.com/api/v1/negotiations/:negotiation_id/expert_neutral_values/:issue_id"
```

# Expert Neutral Profiles

## List Expert Neutral Profiles

> Sample Call

```shell
curl --get "https://go.smartsettle.com/api/v1/expert_neutral_profiles"
```

## Create Expert Neutral Profiles

> Sample Call

```shell
curl --post "https://go.smartsettle.com/api/v1/expert_neutral_profiles"
```

## Update Expert Neutral Profiles

> Sample Call

```shell
curl --put "https://go.smartsettle.com/api/v1/expert_neutral_profiles/:id"
```

## Destroy Expert Neutral Profiles

> Sample Call

```shell
curl --delete "https://go.smartsettle.com/api/v1/expert_neutral_profiles/:id"
```