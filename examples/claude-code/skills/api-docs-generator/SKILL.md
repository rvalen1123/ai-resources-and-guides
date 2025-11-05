# API Documentation Generator

**Version:** 1.0.0  
**Author:** AI Resources Community  
**Description:** Automatically generate comprehensive API documentation from code with OpenAPI/Swagger spec support  
**Created:** 2025-11-05  
**Updated:** 2025-11-05

## Metadata

- **Category:** documentation | development
- **Triggers:** API documentation, API docs, swagger, openapi, REST API docs, generate API documentation
- **Dependencies:** None (uses Claude's native capabilities)
- **Compatibility:** Claude Code IDE | API | Web | All
- **Estimated Duration:** Medium (10-30 min depending on API size)

## Overview

### Purpose
This skill analyzes REST API code and generates comprehensive, professional documentation including endpoint descriptions, request/response schemas, authentication details, and example usage. Supports multiple output formats including Markdown, OpenAPI 3.0, and Swagger 2.0.

### Use Cases
- Generating documentation for new APIs
- Updating documentation after API changes
- Creating OpenAPI specifications for API gateways
- Standardizing API documentation across team
- Onboarding new developers with clear API references

### When to Use This Skill
✅ **Use when:**
- Building REST APIs that need documentation
- Migrating to API-first development
- Creating public API documentation
- Setting up API testing tools (Postman, Insomnia)
- Implementing API versioning

❌ **Don't use when:**
- GraphQL APIs (use GraphQL schema tools)
- Internal function documentation (use code comments)
- Non-HTTP protocols (gRPC, WebSocket - specialized tools needed)

## Instructions

### Prerequisites

**Required:**
- API source code (controllers, routes, handlers)
- Basic understanding of API endpoints

**Optional:**
- Existing documentation to update
- OpenAPI/Swagger specification file
- Example requests/responses
- Authentication flow diagrams

### Workflow Steps

#### 1. API Discovery
**Objective:** Identify all API endpoints and their characteristics

**Actions:**
- Scan code for route definitions (@app.route, app.get, etc.)
- Identify HTTP methods (GET, POST, PUT, DELETE, PATCH)
- Extract endpoint paths and parameters
- Note authentication/authorization requirements
- Identify request/response content types
- Find existing documentation or comments

**Output:** Complete list of endpoints with methods and paths

**Validation:** All routes from code are catalogued

#### 2. Schema Extraction
**Objective:** Document request and response data structures

**Actions:**
- Analyze request body structures (JSON schemas)
- Identify query parameters and path parameters
- Extract response models and status codes
- Document headers (required and optional)
- Note data types and validation rules
- Identify nested objects and arrays
- Extract example values from code or tests

**Output:** Detailed schemas for all request/response bodies

**Validation:** All data fields are documented with types

#### 3. Authentication Documentation
**Objective:** Document security and authentication mechanisms

**Actions:**
- Identify authentication method (JWT, OAuth, API Key, etc.)
- Document authentication flow
- List required headers/tokens
- Document authorization scopes/permissions
- Note rate limiting if applicable
- Document security best practices

**Output:** Complete authentication guide

**Validation:** Clear instructions for API consumers

#### 4. Example Generation
**Objective:** Create working examples for each endpoint

**Actions:**
- Generate curl command examples
- Create sample request bodies
- Show sample responses (success and error)
- Include common use case scenarios
- Add code examples in popular languages (optional)
- Show pagination examples if applicable

**Output:** Copy-paste ready examples

**Validation:** Examples are syntactically correct and realistic

#### 5. Error Documentation
**Objective:** Document all possible error responses

**Actions:**
- List all HTTP status codes used
- Document error response format
- Provide error message examples
- Explain error scenarios
- Include troubleshooting tips
- Document error codes if custom ones exist

**Output:** Complete error reference

**Validation:** All error paths from code are documented

#### 6. Format Generation
**Objective:** Generate documentation in requested format(s)

**Actions:**
- Generate Markdown documentation
- Create OpenAPI 3.0 specification (if requested)
- Generate Swagger 2.0 spec (if requested)
- Create Postman collection (if requested)
- Add interactive examples
- Include table of contents
- Add search/navigation aids

**Output:** Professional, formatted documentation

**Validation:** Documentation passes validation tools

### Error Handling

**Common Issues:**

**Issue:** Incomplete route information
- **Cause:** Routes defined dynamically or in multiple files
- **Solution:** Request additional files or clarify route structure

**Issue:** Missing schema information
- **Cause:** Loosely typed languages or minimal type hints
- **Solution:** Infer from usage or request examples

**Issue:** Inconsistent naming
- **Cause:** Various naming conventions in codebase
- **Solution:** Standardize in documentation, note variations

### Quality Checks

**Before completion, verify:**
- [ ] All endpoints documented with correct HTTP methods
- [ ] Request/response schemas are complete
- [ ] Authentication clearly explained
- [ ] Examples are working and realistic
- [ ] Error responses documented
- [ ] OpenAPI spec validates (if generated)
- [ ] Formatting is consistent and professional

## Examples

### Example 1: Express.js API Documentation

**Context:** Documenting a simple user management API

**Input:**
```javascript
// routes/users.js
router.get('/users', async (req, res) => {
  const { page = 1, limit = 10 } = req.query;
  const users = await User.find().limit(limit).skip((page-1)*limit);
  res.json({ users, page, limit, total: await User.count() });
});

router.post('/users', auth, async (req, res) => {
  const { username, email, password } = req.body;
  const user = await User.create({ username, email, password });
  res.status(201).json({ user });
});

router.get('/users/:id', async (req, res) => {
  const user = await User.findById(req.params.id);
  if (!user) return res.status(404).json({ error: 'User not found' });
  res.json({ user });
});
```

**Process:**
```bash
> Generate API documentation for this user management API
```

**Output:**
```markdown
# User Management API

## Authentication
Most endpoints require JWT authentication. Include the token in the Authorization header:
```
Authorization: Bearer <your-jwt-token>
```

## Endpoints

### List Users
`GET /users`

Retrieve a paginated list of users.

**Query Parameters:**
| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| page | integer | No | 1 | Page number |
| limit | integer | No | 10 | Results per page |

**Response:** `200 OK`
```json
{
  "users": [
    {
      "id": "507f1f77bcf86cd799439011",
      "username": "johndoe",
      "email": "john@example.com"
    }
  ],
  "page": 1,
  "limit": 10,
  "total": 45
}
```

**Example:**
```bash
curl -X GET "https://api.example.com/users?page=1&limit=10"
```

---

### Create User
`POST /users`

🔒 **Requires Authentication**

Create a new user account.

**Request Body:**
| Field | Type | Required | Description |
|-------|------|----------|-------------|
| username | string | Yes | Unique username |
| email | string | Yes | Valid email address |
| password | string | Yes | Min 8 characters |

**Response:** `201 Created`
```json
{
  "user": {
    "id": "507f1f77bcf86cd799439011",
    "username": "johndoe",
    "email": "john@example.com"
  }
}
```

**Example:**
```bash
curl -X POST "https://api.example.com/users" \
  -H "Authorization: Bearer YOUR_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "username": "johndoe",
    "email": "john@example.com",
    "password": "securepass123"
  }'
```

**Error Responses:**
- `401 Unauthorized` - Missing or invalid authentication token
- `400 Bad Request` - Invalid request body
- `409 Conflict` - Username or email already exists

---

### Get User by ID
`GET /users/:id`

Retrieve a specific user by their ID.

**Path Parameters:**
| Parameter | Type | Description |
|-----------|------|-------------|
| id | string | User's unique ID |

**Response:** `200 OK`
```json
{
  "user": {
    "id": "507f1f77bcf86cd799439011",
    "username": "johndoe",
    "email": "john@example.com"
  }
}
```

**Example:**
```bash
curl -X GET "https://api.example.com/users/507f1f77bcf86cd799439011"
```

**Error Responses:**
- `404 Not Found` - User does not exist
```json
{
  "error": "User not found"
}
```

## Error Handling

All error responses follow this format:
```json
{
  "error": "Human-readable error message"
}
```

Common HTTP Status Codes:
- `200 OK` - Request succeeded
- `201 Created` - Resource created successfully
- `400 Bad Request` - Invalid input
- `401 Unauthorized` - Authentication required
- `404 Not Found` - Resource not found
- `409 Conflict` - Resource already exists
- `500 Internal Server Error` - Server error
```

**Result:** Complete, professional API documentation with examples

### Example 2: OpenAPI Specification Generation

**Context:** Generate OpenAPI 3.0 spec for the same API

**Process:**
```bash
> Generate an OpenAPI 3.0 specification for this API
```

**Output:**
```yaml
openapi: 3.0.0
info:
  title: User Management API
  description: API for managing user accounts
  version: 1.0.0
  contact:
    name: API Support
    email: support@example.com

servers:
  - url: https://api.example.com
    description: Production server

security:
  - BearerAuth: []

paths:
  /users:
    get:
      summary: List Users
      description: Retrieve a paginated list of users
      security: []
      parameters:
        - name: page
          in: query
          schema:
            type: integer
            default: 1
          description: Page number
        - name: limit
          in: query
          schema:
            type: integer
            default: 10
          description: Results per page
      responses:
        '200':
          description: Successful response
          content:
            application/json:
              schema:
                type: object
                properties:
                  users:
                    type: array
                    items:
                      $ref: '#/components/schemas/User'
                  page:
                    type: integer
                  limit:
                    type: integer
                  total:
                    type: integer

    post:
      summary: Create User
      description: Create a new user account
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
        '201':
          description: User created successfully
          content:
            application/json:
              schema:
                type: object
                properties:
                  user:
                    $ref: '#/components/schemas/User'
        '400':
          $ref: '#/components/responses/BadRequest'
        '401':
          $ref: '#/components/responses/Unauthorized'

  /users/{id}:
    get:
      summary: Get User by ID
      description: Retrieve a specific user
      security: []
      parameters:
        - name: id
          in: path
          required: true
          schema:
            type: string
      responses:
        '200':
          description: Successful response
          content:
            application/json:
              schema:
                type: object
                properties:
                  user:
                    $ref: '#/components/schemas/User'
        '404':
          $ref: '#/components/responses/NotFound'

components:
  securitySchemes:
    BearerAuth:
      type: http
      scheme: bearer
      bearerFormat: JWT

  schemas:
    User:
      type: object
      properties:
        id:
          type: string
        username:
          type: string
        email:
          type: string
          format: email

  responses:
    BadRequest:
      description: Invalid request
      content:
        application/json:
          schema:
            type: object
            properties:
              error:
                type: string
    Unauthorized:
      description: Authentication required
      content:
        application/json:
          schema:
            type: object
            properties:
              error:
                type: string
    NotFound:
      description: Resource not found
      content:
        application/json:
          schema:
            type: object
            properties:
              error:
                type: string
```

**Result:** Valid OpenAPI 3.0 specification that can be imported into Swagger UI, Postman, or API gateways

## Configuration

### Customization Options

**Parameter:** `output_format`
- **Description:** Documentation format to generate
- **Default:** `markdown`
- **Options:** `markdown | openapi3 | swagger2 | postman | all`
- **Example:** "Generate OpenAPI 3.0 spec for this API"

**Parameter:** `include_examples`
- **Description:** Whether to include curl and code examples
- **Default:** `true`
- **Options:** `true | false`
- **Example:** "Generate API docs without code examples"

**Parameter:** `detail_level`
- **Description:** Amount of detail in documentation
- **Default:** `comprehensive`
- **Options:** `minimal | standard | comprehensive`
- **Example:** "Generate minimal API documentation"

**Parameter:** `language_examples`
- **Description:** Programming languages for code examples
- **Default:** `curl`
- **Options:** `curl | python | javascript | java | go | ruby`
- **Example:** "Include Python and JavaScript examples"

## Resources

### Included Files

This skill uses Claude's native capabilities - no additional files required.

### External Resources

- [OpenAPI Specification](https://swagger.io/specification/) - OpenAPI 3.0 reference
- [Swagger Editor](https://editor.swagger.io/) - Validate OpenAPI specs
- [API Documentation Best Practices](https://swagger.io/resources/articles/best-practices-in-api-documentation/)

## Advanced Usage

### Combining with Other Skills

This skill works well with:
- **Code Reviewer** - Validate API design before documenting
- **Test Generator** - Create API tests from documentation
- **OpenAPI Validator** - Validate generated specifications

### Integration Patterns

**Pattern 1: API-First Development**
```bash
# Generate spec first, implement later
> Create OpenAPI spec for a user authentication API with JWT
```

**Pattern 2: Documentation Update Automation**
```bash
# Update docs after code changes
> Update API documentation to reflect changes in auth.js
```

**Pattern 3: Multi-Format Export**
```bash
# Generate all formats at once
> Generate API docs in Markdown, OpenAPI 3.0, and Postman collection
```

## Testing

### Test Cases

**Test 1: Complete Endpoint Documentation**
- **Setup:** API with various HTTP methods
- **Execute:** Generate documentation
- **Expected:** All endpoints with correct methods documented
- **Verify:** Request/response schemas included

**Test 2: OpenAPI Validation**
- **Setup:** API code with standard patterns
- **Execute:** Generate OpenAPI 3.0 spec
- **Expected:** Valid OpenAPI specification
- **Verify:** Spec passes Swagger validation

**Test 3: Example Generation**
- **Setup:** API with complex nested objects
- **Execute:** Generate docs with examples
- **Expected:** Working curl commands for all endpoints
- **Verify:** Examples can be copied and executed

## Changelog

### Version 1.0.0 (2025-11-05)
- Initial release
- Markdown documentation generation
- OpenAPI 3.0 specification support
- Example generation (curl, Python, JavaScript)
- Error documentation

## Contributing

Enhancements welcome:
1. Add more output formats (AsyncAPI, GraphQL schema)
2. Enhance language example generation
3. Add API testing integration
4. Support more frameworks (FastAPI, Spring, Django)

## License

MIT License - Free to use and modify

## Support

**Questions or Issues?**
- Open an issue with tag `skill:api-docs-generator`
- Include API framework and language
- Share example endpoint code

## Related Skills

- [Code Reviewer](../code-reviewer/) - Validate API design
- [Test Coverage Analyzer](../test-coverage-analyzer/) - Ensure API tests exist

---

**Credits:** Based on OpenAPI specification standards and API documentation best practices.

*This skill is part of the [AI Resources and Guides](https://github.com/rvalen1123/ai-resources-and-guides) repository.*
