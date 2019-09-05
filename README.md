# JWT-authorization-nodeJS

Server:
node server.js // starts server on 8000 port

Now try to make a curl request for home page(/).

Client:
curl -X GET http://localhost:8000
{"success":false,"message":"Auth token is not supplied"}

So our application is preventing us from accessing index without supplying the token. 
Now let us exchange our credentials for the token.

curl --header "Content-Type: application/json" \
  --request POST \
  --data '{"password":"password", "username":"admin"}' \
  http://localhost:8000/login

{
  "success":true,
  "message":"Authentication successful!",
  "token":"eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImFkbWluIiwiaWF0IjoxNTY3NTc1MzA0LCJleHAiOjE1Njc2NjE3MDR9.zjWnyP9-vPvjXNWiXXhDDNT8EOygZd4sCfUaB7SaL8Y"
}

We can remake our last home page request by adding a bearer token.
curl -X GET \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImFkbWluIiwiaWF0IjoxNTY3NTc1MzA0LCJleHAiOjE1Njc2NjE3MDR9.zjWnyP9-vPvjXNWiXXhDDNT8EOygZd4sCfUaB7SaL8Y' \
  http://localhost:8000
{
    "success": true,
    "message": "Index page"
}
