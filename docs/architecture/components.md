# Components

### Component List

#### TodoItem

**Responsibility:** Displays a single to-do item and handles interactions like marking it complete.

**Key Interfaces:**
- `onToggleComplete()`
- `onDelete()`

**Dependencies:** `Todo` type from `packages/shared`.

**Technology Stack:** React, TypeScript, Tailwind CSS.

#### TodoList

**Responsibility:** Renders a list of `TodoItem` components.

**Key Interfaces:**
- `todos`: An array of `Todo` objects.

**Dependencies:** `TodoItem` component.

**Technology Stack:** React, TypeScript.
