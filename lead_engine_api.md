# RoofHero Lead Engine Documentation
Documentation for publishers to ping and post leads to RoofHero's lead engine.  RoofHero has an expansive network of roofing contractors, and will pay for high intent homeowners looking for a roof, as long as their lead journey is TCPA compliant.

If you'd like to apply to be a publisher, email info@roofhero.com.

## Rules we enforce:
* De-duplication.  If a lead comes in with the same address within a 24-hour period, regardless of source, we will not buy it.
* Coverage verification.  If a lead is not in our zone, we will bid back with $0
* Prior-ping verification.  We require the initial ping and the following post to carry the same `external_lead_id`.  We fetch metadata about the lead that was generated during the ping to post to our network of advertisers.
* Payload validation.  Both a ping and post request will fail if any required fields are missing, or if the values are not as defined below.
* Further payload specs are defined below.

## Here is an example PING request:

```
curl --location 'https://www.roofhero.com/external-leads' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer <token>' \
--data '{
"address": "<Street Address>, <City>, <State>", 
"zip": "<zip>",
"roof_material": "<material>",
"home_type": "<home_type>",
"external_lead_id": "<lead_id>",
"type": "PING",
"api_client_name": "<api_client_name>"
}
'
```

### All fields are required for an invocation.  The following values will be provided to you by a RoofHero representative:
```
token
api_client_name
```

### Here are the possible values for all other fields:

`address` (must be a valid address):
```
"<street address>, <city>, <state>"
```

* Note: state must be two-letter abbreviation in ALL CAPS.  Example: "Tennessee" would be "TN".

`zip`: 5 digit string, must be U.S. based.

`roof_material`:
```
"asphalt"
"metal"
"tile"
"cedar_shake"
"flat"
"other"
```

`home_type`:
```
"single family home"
"town home"
```

`external_lead_id`: string. client-created. Must be a unique string, less than 16 characters.

`api_client_name`: string. Provided by RoofHero to client.


A succesful response will look something like this:
```
{
    "message": "Price: 0. Lead ID: test succesfully pinged."
}
```


## Here is an example POST request:

```
curl --location 'https://www.roofhero.com/external-leads' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer <token>' \
--data '{
"address": "<Street Address>, <City>, <State>", 
"zip": "<zip>",
"roof_material": "<material>",
"home_type": "<home_type>",
"price": "<price>",
"first_name": "<first_name>",
"last_name": "<last_name>",
"phone_number": "<phone_number>",
"email": "<email>",
"trusted_cert": "<trusted_cert>",
"external_lead_id": "<lead_id>",
"type": "POST",
"api_client_name": "<api_client_name>"
}
'
```

## Fields unique to POST
* All fields are required.

`price`: float.  in USD dollars.  Example would be `40.58`, representing $40.58.

`first_name`: string. 

`last_name`: string.

`phone_number`: string.  No strict formatting.

`email`: string.

`trusted_cert`: string.

`external_lead_id`: we verify the lead has been pinged before allowing for a post.


A succesful response will look something like this:
```
{
    "message": "Lead ID: <external_lead_id> succesfully posted."
}
```

Please email info@roofhero.com with any questions.
