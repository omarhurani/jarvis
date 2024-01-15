# Authentication Example
An example of an authenticated request is as shown:
```curl
curl -X POST \
 http://127.0.0.1:8000/api/test \
 -H 'Accept: application/json' \
 -H 'Authorization: Bearer {{access_token}}
 -H 'Content-Type: application/json' \
 -d '
    {
        "name":"ttt",
        "websiteURL":"http://T.T",
        "credit":"100",
        "tags":"1",
        "testers":"5",
        "comment":true
    }
'
```
Where \{\{access\_token\}\} is the valid token that is given to the user by the server whenever they log in. It was not placed in the report because its size is massive.

An example of a response to an authenticated request is as shown:
```json
{
   "success": true,
   "data": {
       "name": "ttt",
       "websiteURL": "http://T.T",
       "credit": "100",
       "tags": "1",
       "testers": "5",
       "comment": true,
       "client_id": 1,
       "updated_at": "2019-05-09 20:17:17",
       "created_at": "2019-05-09 20:17:17",
       "id": 5
   },
   "message": "Test created successfully."
}
```
