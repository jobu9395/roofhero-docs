# roofhero-docs
Documentation for contractors to integrate their CRM with RoofHero's instant AI pricing API.

RoofHero's custom API integration is designed for contractors with existing infrastructure to support real time API invocations (typically within their CRM).

After creating a new lead, post to roofhero's API.  This will return a payload with material and address-specific pricing.  The API invocation takes about 1 second.

Here is an example POST request:

```
curl --location 'http://www.roofhero.com/ai-pricing' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer <token>' \
--data '{"address": "<address>", 
"home_type": "single family home",
"map_type": "bing",
"pitch": "flat",
"complexity": "normal",
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

`address` (must be a valid address):
```
street address, city, state, zip
```

`home_type`:
```
town home
single family home
```

`map_type` (recommend keeping set to `bing`):
```
bing
google
mapbox
```

`pitch`:
```
flat
normal
steep
very steep
```

`complexity` (this is waste factor):
```
normal
complex
very complex
```
