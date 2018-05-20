# Our REST API Specification

A big problem for REST APIs is its lack of standard specification. If you put 10 developers in a room and ask them what a REST API is, they are bound to all disagree on something. In order for developers at Hack4Impact to easily pick up, develop, or utilize APIs that are developed by Hack4Impact, we have made a REST API specification for all REST APIs developed inside of Hack4Impact.

## Specification

This specification is not meant to be a stringent one. It's more a specific guideline in parts where standardization would provide more clarity and allow for greater developer velocity cross-team. Our [Inspiration](https://medium.com/@shazow/how-i-design-json-api-responses-71900f00f2db).

### HTTP header functions

* **GET** -- Read a specific resource \(by an identifier\) or a collection of resources. Do not use a payload for this and it must not change any resource.
* **POST** -- Create a new resource. Also a catch-all function for operations that don't fit into the other functions.
* **PUT** -- Update a specific resource \(by an identifier\) or a collection of resources.
* **DELETE** -- Delete a specific resource by an identifier.

### Sensible Resource Names

Creating good resource names will allow frontend developers and yourself easily navigate the API.

1. Use plural nouns, everything as lowercase, and use `_` for spaces

```text
Good: /users
Bad: /user
```

1. Do not use query-string parameters for queries. Only use them for filtering

```text
Good: /users/1
Bad: /users?id=1
```

1. Keep URLs as short as possible

### Response JSON format

Always use JSON as your response since Javascript parses it real fast. **ALL** your responses should look like this:

```text
{
  "code": 200, 
  "message": "", 
  "result": {}, 
  "success": true
}
```

where `result` should hold a dictionary of your data that you want to send. The key of this dictionary should be the result's type and the value should be the actual result data. See a more detailed rationale [here](https://medium.com/@shazow/how-i-design-json-api-responses-71900f00f2db#4bab)

**Status Codes**

Your status codes should be shown in the attribute `code` and in the HTTP Response Header. Here are some main ones:

* **2xx** -- OK
* **4xx** -- Bad Request - identifier doesn't point to any resource, forbidden, missing data, etc.
* **5xx** -- Internal Server Error - server screwed up

**Message**

Messages are made for developers. Make these messages concise but specific to the error they ran into. You may use Exception Errors

**`Success` attribute**

This will be a boolean that will show `success` whenever the status code is 200 to 320.

#### Flask Boilerplate

Flask boilerplate will include a utility helper function to create responses. Look at the code in `/api/utils.py` [here](https://github.com/tko22/flask-boilerplate/blob/master/api/utils.py) for more information on how to use it and how it works.

### Future Improvements

Unless we use status codes extensively, utilizing the different standardized meanings of what codes 201, 203, 404, etc. mean, they don't provide those who are calling the API with much information. Thus, having specific status string codes in the response JSON under a `status`field may be a possibility. The [Google Maps API](https://developers.google.com/places/web-service/details) actually utilizes this. I believe easier development for both developers in backend and frontend teams\(they don't have to look at the documentation to figure out what 304 means\) outweighs the slight disadvantage of string vs integer comparisons \(although javascript string comparison might just be as fast in some scenarios \).

I would suggest having a couple status string code:

* `OK` indicates that no errors occurred
* `UNKNOWN_ERROR` indicates a server-side error; trying again may be successful.
* `REQUEST_DENIED` indicates that your request was denied, generally because of an invalid user
* `INVALID_REQUEST` generally indicates that the query is missing.
* `NOT_FOUND` indicates that the resource was not found
* `EMPTY_RESULT`

However, in some cases, more status string codes may need to be added.

