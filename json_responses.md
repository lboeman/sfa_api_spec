# JSON API response objects
Solar Forecast arbiter API response objects based on the [JSON API](https://jsonapi.org/)

## Observations/Forecasts
Full Resource example.
```
{
	"data":{
		"type": "observations",
		"id": "1234567891011121314",
		"attributes": {
			"name": "Ashland OR",
			"resolution": "1 min",
			"latitude": "42.190000",
			"longitude": "-122.700000",
			"elevation": "595",
			"station_id": "94040",
		    "abbreviation":	"AS",
			"timezone": "Etc/GMT+8",
			"attribution":	"NaN",
			"source": "UO SRML",
		},
		"links":{
			"self": "/observations/1234567891011121314",
		},
		"relationships":{
			"provider":{
				"data":{
					"type": "organizations",
					"id": "10293847561029384756",
				},
			},
		},
	},
	"included": [{
		"type": "organizations",
		"id": "10293847561029384756",
		"attributes":{
			"name": "University of Oregon Solar Radiation Measurement Laboratory",
			"": "",
		},
		"links":{
			"self": "/organizations/10293847561029384756",
		},
	}]	
}
```
### Updating:

Updates are handled with the `PATCH` http verb.

- #### Resources  
To update a resources fields/metadata directly a PATCH request can be made to the resource's uri with the fields you wish to update.   
https://jsonapi.org/format/#crud-updating  
Example: updates the below observation object's timezone to UTC  

```
PATCH /observations/1234567891011121314 HTTP/1.1
Content-Type: application/vnd.api+json
Accept: application/vnd.api+json

{
	"data":{
		"type": "observations",
		"id": "1234567891011121314",
		"attributes": {
			"timezone": "UTC",
		}
	}
}
```
- #### Relationships  
To update relationship between resources a PATCH request can be made to the uri of the resource to which the relationship is assigned.  
https://jsonapi.org/format/#crud-updating-relationships  
Example: Updates provider relationship of a data (observation/forecast) resource.   

```
PATCH: /observations/1234567891011121314/provider
Content-Type: application/vnd.api+json
Accept: application/vnd.api+json

{
	"data": { "type": "organizations", "id": "<uuid>" }
}
```


Organizations
```
{
	"data":{
		"type": "organizations",
		"id": "1029",
		"attributes": {
			"name": "UO SRML",
			# metadata for organizations
		},
		"links":}
			"self": "/organizations/1029",
		},
		"relationships": {
			"users": {
				"data": [
					{"type": "users", "id": "<uuid>"},
					{"type": "users", "id": "<uuid>"},
				] 
			},
			"observations": {
				"data": [
					{"type": "observations", "id": "<uuid>"},
					{"type": "observations", "id": "<uuid>"},
					{"type": "observations", "id": "<uuid>"},
				]
			},
			"forecasts": {
				"data": [
					{"type": "forecasts", "id": "<uuid>"},
					{"type": "forecasts", "id": "<uuid>"},
					{"type": "forecasts", "id": "<uuid>"},
				]
			},
		}
	},
	"included": [
		{
			"type": "users",
			"id": "12",
			"attributes":{
				"name": "Dave",
				...
			},
		},
		...
    ]
}
```
