# Data Models

### Todo

**Purpose:** Represents a single task for a user.

**Key Attributes:**
- `id`: `uuid` - Unique identifier for the task.
- `user_id`: `uuid` - Foreign key to the user who owns the task.
- `title`: `text` - The content of the task.
- `is_complete`: `boolean` - Whether the task is completed.
- `created_at`: `timestamp` - When the task was created.

#### TypeScript Interface

```typescript
export interface Todo {
  id: string;
  userId: string;
  title: string;
  isComplete: boolean;
  createdAt: string;
}
```

#### Relationships

- Belongs to a `User`.
