# to-do Fullstack Architecture Document

## Introduction

This document outlines the complete fullstack architecture for to-do, including backend systems, frontend implementation, and their integration. It serves as the single source of truth for AI-driven development, ensuring consistency across the entire technology stack.

This unified approach combines what would traditionally be separate backend and frontend architecture documents, streamlining the development process for modern fullstack applications where these concerns are increasingly intertwined.

### Starter Template or Existing Project

N/A - Greenfield project

### Change Log

| Date | Version | Description | Author |
| :--- | :--- | :--- | :--- |
| 2025-09-03 | 1.0 | Initial draft generated in YOLO mode. | Winston (Architect) |
| 2025-09-03 | 1.1 | Added sections for Security, Testing, NFR Alignment, and Error Handling based on checklist review. | Winston (Architect) |

## High Level Architecture

### Technical Summary

The architecture for the to-do application will be a modern, serverless, full-stack solution designed for rapid development, scalability, and a great user experience. The overall style is a Jamstack approach, with a Next.js frontend deployed on Vercel and a backend powered by Supabase. This integration provides a seamless development experience with built-in authentication, database, and file storage. This architecture directly supports the PRD goals by enabling a fast, responsive, and reliable application, while staying within a cost-effective, free-tier-friendly infrastructure.

### Non-Functional Requirements Alignment

This architecture directly addresses the Non-Functional Requirements (NFRs) outlined in the PRD:

-   **NFR1 (Fast and Responsive):** The Jamstack architecture with a Next.js frontend hosted on Vercel's edge network ensures minimal latency. Server-side rendering and static generation will be used to deliver content quickly.
-   **NFR2 (iOS and Android):** While the current architecture specifies a web application, Next.js applications are Progressive Web Apps (PWAs) and can be installed on mobile devices. For a native feel, this web codebase can be wrapped in a native shell using tools like Capacitor.
-   **NFR3 (Privacy and Security):** Supabase provides robust security features, including Row Level Security (RLS) on the database and secure JWT-based authentication. All communication is over HTTPS.
-   **NFR4 (Scalability):** Both Vercel and Supabase are built on top of AWS and are designed to scale automatically. The serverless nature of the architecture means we only pay for what we use and can handle large spikes in traffic.
-   **NFR5 (Free-Tier Friendly):** The chosen stack (Vercel, Supabase, Next.js) has generous free tiers that are more than sufficient for an MVP and early-stage growth, aligning with the cost-conscious goal.

### Platform and Infrastructure Choice

**Platform:** Vercel + Supabase
**Key Services:**
- Vercel: Hosting for the Next.js frontend, serverless functions, and CI/CD.
- Supabase: PostgreSQL database, authentication, and file storage.
**Deployment Host and Regions:**
- Vercel: Default (US East)
- Supabase: Default (US East)

### Repository Structure

**Structure:** Monorepo
**Monorepo Tool:** Turborepo
**Package Organization:**
- `apps/web`: The Next.js frontend application.
- `apps/api`: Future placeholder for any custom server-side logic if needed.
- `packages/ui`: Shared React components.
- `packages/shared`: Shared types, validation schemas, and utilities.
- `packages/config`: Shared configuration (ESLint, TypeScript, etc.).

### High Level Architecture Diagram

```mermaid
graph TD
    subgraph User
        A[Student]
    end

    subgraph Vercel Platform
        B[Next.js Web App]
    end

    subgraph Supabase Platform
        C[Supabase Auth]
        D[Supabase DB (PostgreSQL) with RLS]
        E[Supabase Storage]
    end

    A -- Interacts with --> B
    B -- Authenticates with --> C
    B -- Reads/Writes Data --> D
    B -- Stores Files --> E
```

### Architectural Patterns

- **Jamstack Architecture:** Static site generation with serverless APIs - _Rationale:_ Optimal performance and scalability for content-heavy applications.
- **Component-Based UI:** Reusable React components with TypeScript - _Rationale:_ Maintainability and type safety across large codebases.
- **Repository Pattern:** Abstract data access logic - _Rationale:_ Enables testing and future database migration flexibility.
- **API Gateway Pattern:** Single entry point for all API calls - _Rationale:_ Centralized auth, rate limiting, and monitoring.

### Separation of Concerns

-   **UI Layer (View):** Handled by React components within the Next.js `pages` and `components` directories. This layer is responsible for rendering the UI and capturing user input.
-   **Business Logic Layer (Controller/Service):** Implemented within Next.js API Routes (`pages/api`). This layer handles business rules, data validation, and orchestrates calls to the data layer.
-   **Data Access Layer (Model):** Managed by the Supabase client library, which interacts with the PostgreSQL database. The Repository Pattern will be used to abstract the Supabase-specific calls.

## Tech Stack

### Technology Stack Table

| Category | Technology | Version | Purpose | Rationale |
| :--- | :--- | :--- | :--- | :--- |
| Frontend Language | TypeScript | latest | Type safety for the frontend. | Reduces bugs and improves developer experience. |
| Frontend Framework | Next.js | latest | React framework for production. | Provides SSR, SSG, and a great developer experience. |
| UI Component Library | Tailwind CSS | latest | Utility-first CSS framework. | Rapidly build custom designs. |
| State Management | Zustand | latest | Small, fast state-management for React. | Simple and effective for managing global state. |
| Backend Language | TypeScript | latest | Type safety for the backend. | Reduces bugs and improves developer experience. |
| Backend Framework | Next.js API Routes | latest | Serverless functions within Next.js. | Simplifies backend development for a full-stack app. |
| API Style | REST | N/A | Standard for web APIs. | Well-understood and supported. |
| Database | PostgreSQL | latest | Relational database from Supabase. | Powerful and reliable for structured data. |
| Cache | N/A | N/A | Not required for MVP. | Keep it simple. |
| File Storage | Supabase Storage | latest | S3-compatible object storage. | Easy to use with Supabase auth. |
| Authentication | Supabase Auth | latest | Handles user authentication. | Provides a complete solution out of the box. |
| Frontend Testing | Jest & React Testing Library | latest | For unit and component testing. | Standard for React applications. |
| Backend Testing | Jest | latest | For unit testing API routes. | Standard for JavaScript/TypeScript. |
| E2E Testing | Cypress | latest | For end-to-end testing. | Robust and reliable for testing user flows. |
| Build Tool | Turborepo | latest | High-performance build system for monorepos. | Speeds up development in a monorepo. |
| Bundler | Webpack (via Next.js) | latest | Bundles assets for the browser. | Comes with Next.js. |
| IaC Tool | N/A | N/A | Not required for MVP. | Vercel and Supabase provide a simple UI-based setup. |
| CI/CD | Vercel | latest | Continuous deployment for the frontend. | Integrates seamlessly with Next.js and GitHub. |
| Monitoring | Vercel Analytics | latest | For monitoring frontend performance. | Simple and integrated with Vercel. |
| Logging | Vercel Functions Logs | latest | For logging serverless function output. | Simple and integrated with Vercel. |
| CSS Framework | Tailwind CSS | latest | Utility-first CSS framework. | Rapidly build custom designs. |

## Data Models

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

## Database Schema

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

## API Specification

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

## Components

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

## Security

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

## Testing Strategy

### Testing Pyramid

A standard testing pyramid will be followed to ensure a healthy and maintainable test suite.

```
      /\
     /  \   E2E Tests (Cypress)
    /____\
   /      \ Integration Tests (React Testing Library + Jest)
  /________\
 /          \ Unit Tests (Jest)
/____________\
```

-   **Unit Tests:** Focus on individual functions and components in isolation. These will be fast and numerous.
-   **Integration Tests:** Test the interaction between components, such as a form and its submission logic.
-   **E2E Tests:** Test complete user flows from the user's perspective, running in a real browser.

## Error Handling & Resilience

-   **Frontend:** API call errors will be caught in the service layer. The UI will display user-friendly error messages and allow the user to retry the action.
-   **Backend:** API routes will use a centralized error handling middleware. Errors will be logged, and a standardized error response will be sent to the client.
-   **Resilience:** Given the serverless nature of Vercel and Supabase, the infrastructure is inherently resilient. If a function fails, it will not affect other functions.

## Monitoring and Observability

-   **Frontend:** Vercel Analytics will be used to monitor Core Web Vitals and page views.
-   **Backend:** Vercel's function logs will be used for basic logging and debugging of API routes.
-   **Error Tracking:** For more advanced error tracking, a service like Sentry or LogRocket can be integrated in the future.

## Unified Project Structure

```plaintext
to-do/
├── .github/
│   └── workflows/
│       └── ci.yaml
├── apps/
│   └── web/
│       ├── src/
│       │   ├── components/
│       │   ├── pages/
│       │   ├── hooks/
│       │   ├── services/
│       │   ├── stores/
│       │   ├── styles/
│       │   └── utils/
│       ├── public/
│       ├── tests/
│       └── package.json
├── packages/
│   ├── shared/
│   │   ├── src/
│   │   │   ├── types/
│   │   │   └── utils/
│   │   └── package.json
│   ├── ui/
│   │   ├── src/
│   │   └── package.json
│   └── config/
│       ├── eslint/
│       └── typescript/
├── docs/
│   ├── prd.md
│   ├── front-end-spec.md
│   └── architecture.md
├── .env.example
├── package.json
├── turborepo.json
└── README.md
```

## Development Workflow

### Local Development Setup

#### Prerequisites

```bash
# Install Node.js (v18+) and pnpm
brew install node pnpm
```

#### Initial Setup

```bash
# Clone the repository
git clone <repo-url>
cd to-do

# Install dependencies
pnpm install

# Set up environment variables
cp .env.example .env.local
```

#### Development Commands

```bash
# Start all services
pnpm dev

# Run tests
pnpm test
```

### Environment Configuration

#### Required Environment Variables

```bash
# Frontend (.env.local)
NEXT_PUBLIC_SUPABASE_URL=your-supabase-url
NEXT_PUBLIC_SUPABASE_ANON_KEY=your-supabase-anon-key
```

## Coding Standards

### Critical Fullstack Rules

- **Type Sharing:** Always define types in `packages/shared` and import from there.
- **API Calls:** Never make direct HTTP calls - use the service layer.
- **Environment Variables:** Access only through config objects, never `process.env` directly.
- **Error Handling:** All API routes must use the standard error handler.
- **State Updates:** Never mutate state directly - use proper state management patterns.

### Naming Conventions

| Element | Frontend | Backend | Example |
| :--- | :--- | :--- | :--- |
| Components | PascalCase | - | `UserProfile.tsx` |
| Hooks | camelCase with 'use' | - | `useAuth.ts` |
| API Routes | - | kebab-case | `/api/user-profile` |
| Database Tables | - | snake_case | `user_profiles` |

