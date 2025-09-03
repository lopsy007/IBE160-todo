# API Specification

### REST API Specification

```yaml
openapi: 3.0.0
info:
  title: to-do API
  version: 1.0.0
  description: A simple API for managing to-do items.
servers:
  - url: /api
    description: Local development server
paths:
  /todos:
    get:
      summary: Get all todos for the current user
      responses:
        '200':
          description: A list of todos.
          content:
            application/json:
              schema:
                type: array
                items:
                  $ref: '#/components/schemas/Todo'
    post:
      summary: Create a new todo
      requestBody:
        required: true
        content:
          application/json:
            schema:
              type: object
              properties:
                title:
                  type: string
      responses:
        '201':
          description: The created todo.
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Todo'
  /todos/{id}:
    put:
      summary: Update a todo
      parameters:
        - name: id
          in: path
          required: true
          schema:
            type: string
            format: uuid
      requestBody:
        required: true
        content:
          application/json:
            schema:
              type: object
              properties:
                title:
                  type: string
                is_complete:
                  type: boolean
      responses:
        '200':
          description: The updated todo.
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Todo'
    delete:
      summary: Delete a todo
      parameters:
        - name: id
          in: path
          required: true
          schema:
            type: string
            format: uuid
      responses:
        '204':
          description: No content.
components:
  schemas:
    Todo:
      type: object
      properties:
        id:
          type: string
          format: uuid
        user_id:
          type: string
          format: uuid
        title:
          type: string
        is_complete:
          type: boolean
        created_at:
          type: string
          format: date-time
```
