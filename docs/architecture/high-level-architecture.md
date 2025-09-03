# High Level Architecture

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
