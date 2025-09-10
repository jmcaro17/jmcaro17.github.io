## Status Code: SUCCESS 200 (with authorization)

### Query:
```
query {
  getAllClients { clientId }
}
```
### Response:
```
{
  "data": {
    "getAllClients": [
      {
        "clientId": 1002
      },
      {
        "clientId": 1001
      },
      {
        "clientId": 12345
      }
    ]
  }
}
```

### Mutation: (with authorization)
```
mutation ($input: CreateClientSubscriptionInput!) {
  subscribeClientToModel(input: $input)
}
```

Query Variables:
```
{ "input": { "modelId": 1, "clientId": 1 } }
```

### Response:
```
{
  "data": {
    "subscribeClientToModel": true
  }
}
```

## Status Code: BAD_REQUEST 400

### Query:
```
query BadDates {
  svAlertsByDateRange(startDate: "not-a-date", endDate: "2024-01-01") {
    alertId
    remark
  }
}
```

### Response:
```
{
  "errors": [
    {
      "message": "invalid input syntax for type date: \"0NaN-NaN-NaNTNaN:NaN:NaN.NaN+NaN:NaN\"",
      "locations": [
        {
          "line": 2,
          "column": 3
        }
      ],
      "path": [
        "svAlertsByDateRange"
      ],
      "extensions": {
        "code": "INTERNAL_SERVER_ERROR",
        "stacktrace": [
          "QueryFailedError: invalid input syntax for type date: \"0NaN-NaN-NaNTNaN:NaN:NaN.NaN+NaN:NaN\"",
          "    at PostgresQueryRunner.query (#Users#jessecaro#Desktop#AerialView#repo#aerialview-ui-backend#node_modules#typeorm#driver#src#driver#postgres#PostgresQueryRunner.ts:325:19)",
          "    at process.processTicksAndRejections (node:internal#process#task_queues:105:5)",
          "    at async SelectQueryBuilder.loadRawResults (#Users#jessecaro#Desktop#AerialView#repo#aerialview-ui-backend#node_modules#typeorm#query-builder#src#query-builder#SelectQueryBuilder.ts:3808:25)",
          "    at async SelectQueryBuilder.executeEntitiesAndRawResults (#Users#jessecaro#Desktop#AerialView#repo#aerialview-ui-backend#node_modules#typeorm#query-builder#src#query-builder#SelectQueryBuilder.ts:3554:26)",
          "    at async SelectQueryBuilder.getRawAndEntities (#Users#jessecaro#Desktop#AerialView#repo#aerialview-ui-backend#node_modules#typeorm#query-builder#src#query-builder#SelectQueryBuilder.ts:1671:29)",
          "    at async SelectQueryBuilder.getMany (#Users#jessecaro#Desktop#AerialView#repo#aerialview-ui-backend#node_modules#typeorm#query-builder#src#query-builder#SelectQueryBuilder.ts:1761:25)",
          "    at async target (#Users#jessecaro#Desktop#AerialView#repo#aerialview-ui-backend#node_modules#@nestjs#core#helpers#external-context-creator.js:74:28)",
          "    at async Object.svAlertsByDateRange (#Users#jessecaro#Desktop#AerialView#repo#aerialview-ui-backend#node_modules#@nestjs#core#helpers#external-proxy.js:9:24)"
        ]
      }
    }
  ],
  "data": null
}
```

### Sugested response:
```
{
  "errors": [
    {
      "message": "startDate must be a valid ISO 8601 date string",
      "path": ["svAlertsByDateRange"],
      "extensions": {
        "code": "VALIDATION_ERROR",
        "httpStatus": 400,
        "requestId": "abc123"
      }
    }
  ],
  "data": null
}
```

## Status Code: AUTHENTICATION_ERROR 401

### Query:
```
query {
  getAllClients {
    clientId
  }
}
```

### Response:
```
{
  "errors": [
    {
      "message": "Authentication failed. Please provide a valid token.",
      "locations": [
        {
          "line": 2,
          "column": 3
        }
      ],
      "path": [
        "getAllClients"
      ],
      "extensions": {
        "code": "UNAUTHENTICATED",
        "stacktrace": [
          "UnauthorizedException: Authentication failed. Please provide a valid token.",
          "    at JwtAuthGuard.handleRequest (#Users#jessecaro#Desktop#AerialView#repo#aerialview-ui-backend#src#auth#jwt-auth.guard.ts:15:13)",
          "    at #Users#jessecaro#Desktop#AerialView#repo#aerialview-ui-backend#node_modules#@nestjs#passport#dist#auth.guard.js:44:124",
          "    at #Users#jessecaro#Desktop#AerialView#repo#aerialview-ui-backend#node_modules#@nestjs#passport#dist#auth.guard.js:83:24",
          "    at allFailed (#Users#jessecaro#Desktop#AerialView#repo#aerialview-ui-backend#node_modules#passport#lib#middleware#authenticate.js:110:18)",
          "    at attempt (#Users#jessecaro#Desktop#AerialView#repo#aerialview-ui-backend#node_modules#passport#lib#middleware#authenticate.js:183:28)",
          "    at strategy.fail (#Users#jessecaro#Desktop#AerialView#repo#aerialview-ui-backend#node_modules#passport#lib#middleware#authenticate.js:314:9)",
          "    at #Users#jessecaro#Desktop#AerialView#repo#aerialview-ui-backend#node_modules#passport-jwt#lib#strategy.js:106:33",
          "    at module.exports [as verify] (#Users#jessecaro#Desktop#AerialView#repo#aerialview-ui-backend#node_modules#jsonwebtoken#verify.js:70:12)",
          "    at module.exports [as JwtVerifier] (#Users#jessecaro#Desktop#AerialView#repo#aerialview-ui-backend#node_modules#passport-jwt#lib#verify_jwt.js:4:16)",
          "    at #Users#jessecaro#Desktop#AerialView#repo#aerialview-ui-backend#node_modules#passport-jwt#lib#strategy.js:104:25"
        ],
        "originalError": {
          "message": "Authentication failed. Please provide a valid token.",
          "error": "Unauthorized",
          "statusCode": 401
        }
      }
    }
  ],
  "data": null
}
```

### Mutation:
```
mutation Login($data: LoginDto!) {
  login(data: $data)
}
```

query variables:
```
{
  "data": {
    "email": "test.user@gmail.com",
    "password": "wrongpassword"
  }
}
```

### Response:
```
{
  "errors": [
    {
      "message": "Invalid credentials",
      "locations": [
        {
          "line": 2,
          "column": 3
        }
      ],
      "path": [
        "login"
      ],
      "extensions": {
        "code": "UNAUTHENTICATED",
        "stacktrace": [
          "UnauthorizedException: Invalid credentials",
          "    at AuthService.login (#Users#jessecaro#Desktop#AerialView#repo#aerialview-ui-backend#src#auth#auth.service.ts:34:13)",
          "    at process.processTicksAndRejections (node:internal#process#task_queues:105:5)",
          "    at async AuthResolver.login (#Users#jessecaro#Desktop#AerialView#repo#aerialview-ui-backend#src#auth#auth.resolver.ts:15:20)",
          "    at async target (#Users#jessecaro#Desktop#AerialView#repo#aerialview-ui-backend#node_modules#@nestjs#core#helpers#external-context-creator.js:74:28)",
          "    at async Object.login (#Users#jessecaro#Desktop#AerialView#repo#aerialview-ui-backend#node_modules#@nestjs#core#helpers#external-proxy.js:9:24)"
        ],
        "originalError": {
          "message": "Invalid credentials",
          "error": "Unauthorized",
          "statusCode": 401
        }
      }
    }
  ],
  "data": null
}
```

# TO-DO:
## Status Code: FORBIDDEN 403 (client not admin)

### Query:
```
query {
  getAllClients { clientId }
}
```

### Response:


### Mutation:
```
mutation ($input: CreateClientSubscriptionInput!) {
  subscribeClientToModel(input: $input)
}
```

query variables:
```
{ "input": { "modelId": 1, "clientId": 1 } }
```
### Response:


## Status Code: NOT FOUND 404

### Query:
```
query MissingAlert {
  svAlert(
    modelId: 999999
    instanceId: 999999
    tradeDate: "1999-01-01"
    alertId: 999999
  ) {
    alertId
    clientId
    modelId
    instanceId
    tradeDate
    remark
  }
}
```

### Response:
```
{
  "errors": [
    {
      "message": "Alert not found",
      "locations": [
        {
          "line": 2,
          "column": 3
        }
      ],
      "path": [
        "svAlert"
      ],
      "extensions": {
        "code": "INTERNAL_SERVER_ERROR",
        "stacktrace": [
          "Error: Alert not found",
          "    at SvAlertService.findOne (#Users#jessecaro#Desktop#AerialView#repo#aerialview-ui-backend#src#services#sv-alert.service.ts:44:13)",
          "    at process.processTicksAndRejections (node:internal#process#task_queues:105:5)",
          "    at async target (#Users#jessecaro#Desktop#AerialView#repo#aerialview-ui-backend#node_modules#@nestjs#core#helpers#external-context-creator.js:74:28)",
          "    at async Object.svAlert (#Users#jessecaro#Desktop#AerialView#repo#aerialview-ui-backend#node_modules#@nestjs#core#helpers#external-proxy.js:9:24)"
        ]
      }
    }
  ],
  "data": null
}
```

## This can be improved:

### Current form:
```
{
  "errors": [
    {
      "message": "Alert not found",
      "path": ["svAlert"],
      "extensions": { "code": "INTERNAL_SERVER_ERROR" }
    }
  ],
  "data": null
}
```

### Suggested form:
```
{
  "errors": [
    {
      "message": "Subscription not found",
      "path": ["updateClientSubscription"],
      "extensions": {
        "code": "NOT_FOUND",
        "httpStatus": 404,
        "requestId": "c7df1e3e-7a2e-4d1e-8f2e-9cf3a1d3b6a0",
        "details": { "modelId": 999999 }
      }
    }
  ],
  "data": null
}
```

### Mutation:
```
mutation BadModelId {
  subscribeToModel(modelId: -1)
}
```

### Response:
```
{
  "data": {
    "subscribeToModel": false
  }
}
```

### Mutation:
```
mutation UnsubMissing {
  unsubscribeFromModel(modelId: -1200)
}
```

### Response:
```
{
  "data": {
    "unsubscribeFromModel": true
  }
}
```

### Show standard form above?

## Status Code: INTERNAL_SERVER_ERROR 500

### Query:
```
query {
  getAllClients { clientId }
}
```

### Response:
```
{
  "errors": [
    {
      "message": "connect ETIMEDOUT 172.16.78.11:5432",
      "locations": [
        {
          "line": 2,
          "column": 3
        }
      ],
      "path": [
        "getAllClients"
      ],
      "extensions": {
        "code": "INTERNAL_SERVER_ERROR",
        "stacktrace": [
          "Error: connect ETIMEDOUT 172.16.78.11:5432",
          "    at TCPConnectWrap.afterConnect [as oncomplete] (node:net:1637:16)"
        ]
      }
    }
  ],
  "data": null
}
```

### Suggested form:
```
{
  "errors": [
    {
      "message": "Something went wrong",
      "path": ["getAllClients"],
      "extensions": {
        "code": "INTERNAL_SERVER_ERROR",
        "httpStatus": 500,
        "requestId": "47a52f31-29df-4cf6-93aa-02c94ad0a245"
      }
    }
  ],
  "data": null
}
```
