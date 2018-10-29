# JSON API response objects
Solar Forecast arbiter API response objects based on the [JSON API](https://jsonapi.org/)

Observations/Forecasts
```
{
	"data":{
		"type": "observations",				# data type/ api path
		"id": "1234567891011121314",		# uuid
		"attributes": {                     # db fields
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
				"data":{							# id/type of organization that provided the data
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
Updates:
	Resources:
	```
	https://jsonapi.org/format/#crud-updating
	example: updates the below observation object's timezone to UTC

		PATCH /observations/<uuid> HTTP/1.1
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
Relationships:
	https://jsonapi.org/format/#crud-updating-relationships
	example: updates provider to different 
	```
		PATCH: /observations/<uuid>/provider
		Content-Type: application/vnd.api+json
		Accept: application/vnd.api+json

		{
			"data": { "type": "organizations", "id": "<uuid>" }
		}
	```


ORGANIZATIONS
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
					{"type": "users", "id": "12"}, #probably a uuid instead of 2 digit number
					{"type": "users", "id": "13"},
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
