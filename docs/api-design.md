---
title: API Design
date: 2021-03-03
slug: designg

---
Netlify light CMS API Contract
Version: v1.0.0 Status: Proposal

**Content Negotiation**

Clients MUST send all JSON data in request documents with the header `Content-Type: application/json`

#### Server Responsibilities

The server will return only `JSON` documents `Content-Type: application/json)`

**Success Responses Format**

* `GET`: Get a single Resource

    200 - Ok
    {
    	data: {Resource Object}
    	errors: nil
    	meta: {
    		"status_code": 200
    	}
    }
    

* `GET`: Get a list of Resources

    200 - Ok
    {
    	data: [
    		{Resource Object}
    	]
    	errors: nil
    	meta: {
    		"status_code": 200
    	}
    }
    

* `POST`: Create a Resource

    201 - Created
    {
    	data: {Resource Object}
    	errors: nil
    	meta: {
    		"status_code": 201
    	}
    }
    

* `PUT`, `PATCH`: Update a Resource

    200 Ok
    {
    	data: {Resource Object}
    	errors: nil
    	meta: {
    		"status_code": 200
    	}
    }
    

* `DELETE`: Delete a Resource

    204 No Content
    {
    	data: nil
    	errors: nil
    	meta: {
    		"status_code": 204
    	}
    }
    

**Error Responses Format**

* Generic format

    {
    	data: nil,
    	errors: [
    		{
    			title: "Error's generic title"
    			detail: "Error's Details",
    			source: "Part of the request document caused the error",
    			status: Error's Status
    		}
    	],
    	meta: {
    		"status_code": Error's code
    	}
    }
    

**Error codes**

* `400 Bad Request`: The request was not processed. The server could not understand what the request is asking for
* `401 Unauthorized` indicates that the client is not allowed to access resources
* `403 Forbidden` The request is valid and authenticated, but the client is not allowed access the resource for any reason.
* `404 Not Found` The requested resource is not available now.
* `409 Conflict` This response is sent when a request conflicts with the current state of the server.
* `412 Precondition Failed` The request have certain preconditions in the headers which the server does not meet.
* `422 Unprocessable Entity` The server understands the content type of the request entity, but was unable to process the contained instructions.
* `500 Internal Server Error` The request is valid, but the server is asked to serve some unexpected condition.
* 