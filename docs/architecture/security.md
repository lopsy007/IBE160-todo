# Security

### Authentication

Authentication will be handled by Supabase Auth. Users will be able to sign up and log in using email and password. The Supabase client library will manage JWTs, which will be sent with every request to the backend.

### Authorization

Authorization will be enforced at the database level using Supabase's Row Level Security (RLS). Policies will be created to ensure that users can only access and modify their own data.

Example RLS Policy for `todos`:
```sql
-- Users can only see their own todos.
CREATE POLICY "Enable read access for own user" ON "public"."todos"
AS PERMISSIVE FOR SELECT
TO authenticated
USING (auth.uid() = user_id);

-- Users can only create todos for themselves.
CREATE POLICY "Enable insert for own user" ON "public"."todos"
AS PERMISSIVE FOR INSERT
TO authenticated
WITH CHECK (auth.uid() = user_id);
```

### API Security

-   All API routes will be protected and require a valid JWT.
-   Input validation will be performed on all incoming requests to prevent injection attacks.
-   Rate limiting will be handled by Vercel's infrastructure.
