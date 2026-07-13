# Exercise: API Documentation

## Original API Endpoint Code

**Selected Example:** Python/Flask User Registration API

```python
@app.route('/api/users/register', methods=['POST'])
def register_user():
    """Register a new user"""
    data = request.get_json()

    required_fields = ['username', 'email', 'password']
    for field in required_fields:
        if field not in data:
            return jsonify({
                'error': 'Missing required field',
                'message': f'{field} is required'
            }), 400

    if User.query.filter_by(username=data['username']).first():
        return jsonify({
            'error': 'Username taken',
            'message': 'Username is already in use'
        }), 409

    if User.query.filter_by(email=data['email']).first():
        return jsonify({
            'error': 'Email exists',
            'message': 'An account with this email already exists'
        }), 409

    if not re.match(r"^[^@]+@[^@]+\.[^@]+$", data['email']):
        return jsonify({
            'error': 'Invalid email',
            'message': 'Please provide a valid email address'
        }), 400

    if len(data['password']) < 8:
        return jsonify({
            'error': 'Weak password',
            'message': 'Password must be at least 8 characters long'
        }), 400

    ...
```

# Prompt 1: Comprehensive Endpoint Documentation
## AI Prompt Used

> Please create comprehensive documentation fo rhis API endpoint.

## User Registration API
Registers a new user account in the application. The endpoint validates user input, checks for duplicate usernames and email addresses, securely hashes the user's password, stores the account in the database, and returns the newly created user information.

## Endpoint
```
POST /api/users/register
```

## Authentication

No authentication is required because this endpoint is intended for new user registration.

## Request Body

| Field | Type | Required | Description |
|--------|------|----------|-------------|
| username | String | Yes | Unique username for the account |
| email | String | Yes | Valid email address |
| password | String | Yes | Password containing at least 8 characters |

## Authentication

No authentication is required because this endpoint is intended for new user registration.

## Request Body

| Field | Type | Required | Description |
|--------|------|----------|-------------|
| username | String | Yes | Unique username for the account |
| email | String | Yes | Valid email address |
| password | String | Yes | Password containing at least 8 characters |

### Example Request

```json
{
    "username": "mokgadi",
    "email": "mokgadi@example.com",
    "password": "SecurePass123"
}
```

## Success Response

**Status Code**

```
201 Created
```

### Example Response

```json
{
    "message": "User registered successfully",
    "user": {
        "id": 101,
        "username": "mokgadi",
        "email": "mokgadi@example.com",
        "created_at": "2026-07-13T10:30:00",
        "role": "user"
    }
}
```

## Error Responses

| Status | Error | Description |
|---------|-------|-------------|
|400|Missing required field|One or more required fields were not supplied.|
|400|Invalid email|The email format is incorrect.|
|400|Weak password|Password is shorter than 8 characters.|
|409|Username taken|Username already exists.|
|409|Email exists|Email address already exists.|
|500|Server error|Unexpected server or database error.|

### Example Error Response

```json
{
    "error": "Weak password",
    "message": "Password must be at least 8 characters long"
}
```

---

## Example Requests

### Register a New User

```
POST /api/users/register
```

```json
{
    "username":"mokgadi",
    "email":"mokgadi@example.com",
    "password":"SecurePass123"
}
```

### Response

```json
{
    "message":"User registered successfully",
    "user":{
        "id":101,
        "username":"mokgadi",
        "email":"mokgadi@example.com",
        "role":"user"
    }
}
```

### Attempt Registration with Existing Username

```
POST /api/users/register
```

```json
{
    "username":"mokgadi",
    "email":"another@example.com",
    "password":"SecurePass123"
}
```

### Response

```json
{
    "error":"Username taken",
    "message":"Username is already in use"
}
```

## Rate Limiting/Special Considerations
- Passwords are hashed before being stored.
- Email addresses are stored in lowercase.
- Confirmation emails are sent after successful registration.
- Duplocate usernames and email addresses are not allowed.
- Input validation occurs before the user is created.



# Prompt 2: Convert to OpenAPI Format
## AI Prompt Used
> Please convert this API information into an OpenAI document.

```yaml
openapi: 3.0.0

info:
  title: User Registration API
  version: 1.0.0
  description: API endpoint for registering new users.

paths:
  /api/users/register:
    post:
      summary: Register a new user
      description: Creates a new user account.

      requestBody:
        required: true
        content:
          application/json:
            schema:
              type: object
              required:
                - username
                - email
                - password
              properties:
                username:
                  type: string
                email:
                  type: string
                  format: email
                password:
                  type: string
                  minLength: 8

      responses:
        "201":
          description: User successfully created.

        "400":
          description: Invalid request.

        "409":
          description: Username or email already exists.

        "500":
          description: Internal server error.
```



# Prompt 3: Developer Usage Guide
## AI Prompt Used

> Please create a developer guide for using our API

# User Registration Developer Guide.
## Getting Started
The User Regristration API allows developers to create new user accounts by sending a POST request to the registration endpoint.

### Base Endpoint
```
POST /api/users/register
```

Authentication is **not required** for this endpoint.

## Registering a User
Send a JSON request containing:
- username
- email
- password
If validation succeeds, the API creates the account and returns the new user information.

## Common Errors
| Problem | Solution |
|----------|----------|
|Missing required field|Provide username, email and password.|
|Invalid email|Use a correctly formatted email address.|
|Weak password|Use at least 8 characters.|
|Username exists|Choose another username.|
|Email already exists|Register with a different email address.|

## Best Practices
- Validate user input before sending requests.
- Always use HTTPS.
- Store authentication credentials securely after registration.
- Display server validation messages to users.
- Handle all possible HTTP status codes in your application.

# Reflection
## Which parts of the API were most challenging to document?
The error handling section was the most detailed becuase multiple validation checks produce different HTTP status codes and messages. Care was needed to document each scenario accurately.

## How did you adjust your prompts to get bettwe results?
I asked the AI to include request parameters, response examples, authentication requirements, error codes, and practical examples. This produced more complete documentation than a general prompt.

## Which documentation format was most effective?
Markdown was the easiet format for developers to read, while OpenAI provided a standardized specification that could be used with API documentation tools such as Swagger.

## How would you incomporate this approach into your workflow?
I would use AI to generation API documentation whenever new endpoints are created. After reviewing the generated content for accuracy, I would maintain both Markdown documentatopn for developers and an OpenAI specification for automated tools.
