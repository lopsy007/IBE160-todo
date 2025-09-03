# Database Schema

The following SQL DDL defines the schema for the `todos` table in the PostgreSQL database.

```sql
CREATE TABLE public.todos (
  id uuid DEFAULT gen_random_uuid() NOT NULL,
  created_at timestamp with time zone DEFAULT now() NOT NULL,
  title text,
  is_complete boolean,
  user_id uuid
);

ALTER TABLE public.todos ADD CONSTRAINT todos_pkey PRIMARY KEY (id);

ALTER TABLE public.todos ADD CONSTRAINT todos_user_id_fkey FOREIGN KEY (user_id) REFERENCES auth.users(id) ON DELETE CASCADE;
```
