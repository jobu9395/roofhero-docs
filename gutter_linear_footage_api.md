# roofhero-docs
Documentation for contractors to integrate their CRM with RoofHero's instant AI gutter linear footage API.

RoofHero's custom API integration is designed for contractors with existing infrastructure to support real time API invocations (typically within their CRM).

After creating a new lead, post to roofhero's API.  This will return a payload with the linear footage.  The API invocation takes ~1-3 seconds.

The linear footage returned includes estimated downspout length.

Here is an example POST request:

```
curl --location 'https://www.roofhero.com/ai-pricing-gutters' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer <token>' \
--data '{"address": "<address>", 
"home_type": "single family home",
"shape": "normal",
"num_stories": 2,
"api_client_name": "<api_client_name>"
}
'
```

All fields are required for an invocation.  The following values will be provided to you by a RoofHero representative:
```
token
api_client_name
```

Here are the possible values for all other fields:

`address` (must be a valid address).  State abbreviation MUST be capitalized.
```
"<street address>, <city>, <state>, <zip>"
```

`home_type`:
```
"town home"
"single family home"
```

`shape`:
```
"normal"
"gable"
"mapbox"
```

`num_stores`:
```
1
2
3
```

A succesful response will look something like this:
```
{
    "gutter_linear_footage": 241,
}
```

Please email info@roofhero.com with any questions.
