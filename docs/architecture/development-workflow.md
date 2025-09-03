# Development Workflow

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
