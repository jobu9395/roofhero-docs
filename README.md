# roofhero-docs
Documentation for contractors to integrate their CRM with RoofHero's instant AI pricing API.

RoofHero's custom API integration is designed for contractors with existing infrastructure to support real time API invocations (typically within their CRM).

After creating a new lead, post to roofhero's API.  This will return a payload with material and address-specific pricing.  The API invocation takes ~1-3 seconds.

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

A succesful response will look something like this:
```
{
    "ai_method": "geo-ai",
    "pricing": {
        "contractor_email": "info@roofhero.com",
        "price_per_square_foot": {
            "asphalt_price": 5.0,
            "cedar_shake_price": 15.0,
            "flat_price": 20.0,
            "metal_price": 12.0,
            "other_price": 20.0,
            "repair_price": 299.0,
            "tile_price": 12.0
        },
        "replacement_prices": {
            "asphalt_price": "$25,418",
            "cedar_shake_price": "$76,253",
            "flat_price": "$101,670",
            "metal_price": "$61,002",
            "other_price": "$101,670",
            "tile_price": "$61,002"
        }
    },
    "roof area": "5,084"
}
```

Please email info@roofhero.com with any questions.

