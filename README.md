# HyperVerge Matching API Documentation (beta)

## Overview

This documentation describes the matching API. The postman collection can be found [here](https://www.getpostman.com/collections/4c9690b3999210129596). 


- [HyperVerge Match Fields API Documentation](#hyperverge-validation-api-documentation-beta)
	- [Overview](#overview)
	- [Schema](#schema)
	- [Parameters](#parameters)
	- [Root Endpoint](#root-endpoint)
	- [Authentication](#authentication)
	- [API Call structure](#api-call-structure)
	- [Request structure](#request-structure)
	- [Response Structure](#response-structure)
	- [Supported Fields](#supported-fields)

## Schema

It is recommended that HTTPS is used for all API calls. For HTTPS, only TLS v1.2 is supported to ensure better security. All data is received as JSON.

## Parameters
All optional and compulsory parameters are passed as part of the request body.

## Root Endpoint
A `GET` request can be issued to the root endpoint to check for successful connection. 

	 curl https://ind-verify.hyperverge.co/api/

The `plain/text` reponse of `Aok` should be received.

## Authentication

Currently, an appId, appKey combination is passed in the request header. The appId and appKey are provided on request by the HyperVerge team. If you would like to try the API, please reach out to contact@hyperverge.co

	curl -X POST https://ind-verify.hyperverge.co/api/matchFields\
	  -H 'appid: xxx' \
	  -H 'appkey: yyy' \
	  -H 'content-type: application/json;' \
	  -d '{}' \


On failed attempt with invalid credentials or unauthorized access the HTTP response would have a status code : 401

Please do not expose the appid and appkey on browser applications. In case of a browser application, set up the API calls from the server side.

## API Call structure


* **URL**
  - /api/matchFields
  
* **Method**
	`POST`
	
* **Header**
	* content-type : application/json
	* appId
	* appKey
	* transactionid

* **Request Body**
	* A combination of one or more of [these](#supported-fields) fields are allowed
		Each field should have the following keys
			* *value1*
			* *value2*
			
## Request Structure

### MatchField
```
{
	“name": {
		“value1": “Sanchit Mehta",
		“value2": "Sanchit Kumar Mehta",
	},
	“address": {
		“value1": “avdflkahdflhd”,
		"value2": “adfbbfjbdfjwjefb",
	},
	“pan_no": {
		“value1": "CHWPM8FAKE",
		“value2": “CHWPM9FAKE",
	},

}
```

## Response Structure

* Success Response:

	* Code: 200 

	* Incase of a successful match of all, the response would have the following schema.
	```
	{
		“status”:”success”
		“statusCode”:”200”
		“result” : {
			“pan_no” : “true”,
			“name” : “true”,
			“address”:”true”,
			“all”: “true"
		}
	}
  ```
	* Incase the successful match of a few fields, the *all*  parameter would be set to false
  
 	
 ```
	{
		“status”:”success”
		“statusCode”:”200”
		“result” : {
			“pan_no” : “no”,
			“name” : “yes”,
			“address”:”yes”,
			“all”: “no"
		}
	}
  ```
 
* Error Responses:
	 
	 * Incase of invalid request, the HTTP code `400` is returned.	 	
  ```	 	
  {
    "status": "failure",
    "statusCode": "400",
    "error": {
      "code" : <Error code>
      "message" : <Error message>
    }
  }
  ```

## Supported Fields
Following are the fields that are supported by the API. Exact key words to be used in the request body are also mentioned below. 

| Field | Key Word |Default Match Type|
|---|---|---|
| Name|name|Fuzzy Match|
|Address|address|Fuzzy Match|
|Pin Code|pin|Direct Match|
|Phone Number|phone|Direct Match|
|Date of Birth|dob|Direct Match|
|Year of Birth|yob|Direct Match|
|Gender|gender|Direct Match|
|Mother's Name|mother|Direct Match|
|Father's Name|father|Direct Match|
|Husband's Name|husband|Direct Match|
|PAN Number|pan_no|Direct Match|
|Aadhaar Number|aadhaar|Direct Match|
|Passport Number|passport_num|Direct Match|
|Voter ID|voterid|Direct Match|
|Place of Birth|place_of_birth|Direct Match|
|Place of Issue|place_of_issue|Direct Match|
|Given Name|given_name|Direct Match|
|Surname|surname|Direct Match|
|Date of Expiry|doe|Direct Match|
|Relation|relation|Direct Match|
|Date for Calculation of Age|doc|Direct Match|
|Age|age|Direct Match|
