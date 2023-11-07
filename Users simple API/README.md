# Users simple API

1. Run json-server on port 3004 with db.json
2. Check that your mock is up and running:

```cURL
curl --location 'http://localhost:3004/users'
```

3. Create Data Graph by sending OAS spec to Dashboard API endpoint:

```cURL
curl --location 'http://localhost:3000/api/data-graphs/data-sources/import' \
--header 'Authorization: <YOUR DASHBOARD AUTH KEY>' \
--header 'Content-Type: application/json' \
--data '{
    "type": "openapi",
    "data": <OAS stringified>
}'
```

If you're using Postman you can stringify your OAS yaml with a simple 'Pre-request Script'.

```bash
pm.environment.set("oas_document", JSON.stringify(`<your yaml>`))
```

Then the request you will be sending will be:

```cURL
curl --location 'http://localhost:3000/api/data-graphs/data-sources/import' \
--header 'Authorization: <YOUR DASHBOARD AUTH KEY>' \
--header 'Content-Type: application/json' \
--data '{
    "type": "openapi",
    "data": {{oas_document}}
}'
```

## Try it out

Try out a query:

```gql
query myQuery{
  getUserById(id: 5) {
    cart_id
    email
    id
    username
  }
}
```

Try out a mutation:

```gql
mutation myMutation ($user_input: UserInput!)  {
  createUser(userInput: $user_input) {
    cart_id
    email
    id
    username
  }
}
```

Variables:

```gql
{
  "user_input": {
    "cart_id": 1,
    "email": "aga@aga.com",
    "id": 201,
    "username": "Aga"
  }
}
```
