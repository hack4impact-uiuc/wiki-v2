# What's a REST API?

**Copied from my** [**Blog post**](https://medium.com/@timmykko/best-way-to-use-django-rest-api-a4ab3218d1ac)

Essentially, an API is the interface the server/backend provides so that apps can talk to them. A **REST API** is an API that follows a set of rules called REST\(Representational State Transfer\) and an API endpoint are certain functions of the interface. It provides endpoints to retrieve, add, update, or delete resources from your database.

Let’s take Instagram for an example, who published their API to the public. So say you wanted to know information about user 1234567, his/her name, how many followers they have, their bio, etc. Given an ACCESS-TOKEN that you get from Instagram, you make a request to an endpoint:

[https://api.instagram.com/v1/users/12345678/?access\_token=ACCESS-TOKEN](https://api.instagram.com/v1/users/12345678/?access_token=ACCESS-TOKEN)

Instagram web servers will then perform certain functions that include searching through their database to get that user and will then return this text, which is in JSON format:

```text
{
 “data”: {
     “id”: “1234567”,
     “username”: “snoopdogg”,
     “full_name”: “Snoop Dogg”,
     “profile_picture”: "http://distillery.s3.amazonaws.com/profiles/profile_1574083_75sq_1295469061.jpg",
     “bio”: “This is my bio”,
     “website”: “http://snoopdogg.com",
     “counts”: {
         “media”: 1320,
         “follows”: 420,
         “followed_by”: 3410
     }
  }
}
```

In addition, REST API leverages the use of different HTTP requests especially `GET`,`POST`,`PUT`,`DELETE`. For the specific endpoint above, you would use `GET` to retrieve information, `POST` to add a new user\(you wouldn't include the `/1234567` though\), `PUT` to modify the user, and `DELETE` to delete the user.

### Outside Resources

* [What's REST](http://www.restapitutorial.com/lessons/restquicktips.html)

