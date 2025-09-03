# Unified Project Structure

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
