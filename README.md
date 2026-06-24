# Integreate

**Feed your schema. Get your API. Bridge your platforms.**

Integreate is an open-source agentic platform that ingests database schemas and automatically generates production-ready API endpoints — and goes further by intelligently mapping and bridging schemas across different platforms so they can talk to each other.

---

## The Problem

Building APIs from a database schema is repetitive, time-consuming, and largely mechanical. Integrating two different platforms — say, a hospital EMR and a lab system, or Salesforce and a custom CRM — takes weeks of senior engineering time: field mapping, data transformation logic, auth negotiation, and endless back-and-forth planning.

Integreate automates both.

---

## What It Does

### 1. Schema → API Generation
Feed Integreate a database schema. It parses your entities, relationships, and field types, then generates a full set of REST API endpoints — controllers, services, DTOs, and validation — ready to drop into your project.

```bash
integreate generate --schema ./schema.prisma --output ./src/api
```

### 2. Cross-Platform Integration Bridging *(coming soon)*
Feed Integreate two schemas from different platforms. It semantically maps fields across them, identifies relationship gaps, proposes transformation rules, and generates the adapter/middleware code to connect them — with a confidence score and a human approval step before anything touches production.

```bash
integreate bridge --schema-a ./dhis2.sql --schema-b ./openmrs.sql --output ./src/bridge
```

---

## Supported Schema Formats

| Format | Status |
|--------|--------|
| SQL DDL | ✅ Supported |
| Prisma Schema | ✅ Supported |
| JSON Schema | 🔜 Coming soon |
| OpenAPI / Swagger | 🔜 Coming soon |
| GraphQL SDL | 🔜 Coming soon |

---

## Generated Output

Integreate generates **NestJS** modules by default, with more framework targets on the roadmap.

For each entity in your schema, you get:

- `entity.controller.ts` — REST endpoints (GET, POST, PATCH, DELETE)
- `entity.service.ts` — Business logic layer
- `entity.dto.ts` — Validated DTOs with class-validator decorators
- `entity.module.ts` — NestJS module wiring
- `entity.entity.ts` — TypeORM entity class

---

## Quick Start

```bash
# Install the CLI
npm install -g @integreate/cli

# Generate API from a Prisma schema
integreate generate --schema ./prisma/schema.prisma --output ./src/generated

# Or from a SQL DDL file
integreate generate --schema ./database.sql --output ./src/generated
```

> **Self-hosted:** Integreate runs entirely on your machine. Your schemas never leave your environment unless you opt into the cloud platform.

---

## Example

Given this schema:

```sql
CREATE TABLE users (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  email VARCHAR(255) UNIQUE NOT NULL,
  name VARCHAR(100),
  created_at TIMESTAMP DEFAULT NOW()
);

CREATE TABLE posts (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  title VARCHAR(255) NOT NULL,
  content TEXT,
  author_id UUID REFERENCES users(id),
  created_at TIMESTAMP DEFAULT NOW()
);
```

Integreate generates a full NestJS CRUD module for both `User` and `Post`, including the relationship, pagination, filtering, and validation — in seconds.

---

## Roadmap

- [x] SQL DDL schema parsing
- [x] Prisma schema parsing
- [x] NestJS CRUD generation
- [ ] JSON Schema & OpenAPI input support
- [ ] Cross-platform schema mapping (bridge mode)
- [ ] Confidence scoring for field mappings
- [ ] Visual approval UI for generated bridges
- [ ] Express.js and Fastify output targets
- [ ] FHIR / HL7 schema support (health systems)
- [ ] Cloud-hosted platform (Integreate Cloud)

---

## Tech Stack

- **Runtime:** Node.js / TypeScript
- **Backend Framework:** NestJS
- **ORM:** Prisma
- **AI Layer:** Anthropic Claude API (semantic schema understanding)
- **Queue:** BullMQ (async generation jobs)
- **Frontend:** Next.js (cloud dashboard)

---

## Contributing

Integreate is MIT-licensed and built in the open. Contributions are welcome.

```bash
git clone https://github.com/integreate-dev/core.git
cd core
npm install
npm run dev
```

See [CONTRIBUTING.md](./CONTRIBUTING.md) for guidelines.

---

## License

MIT © [Integreate](https://integreate.dev)

---

<p align="center">
  Built to eliminate the integration tax — for developers everywhere.
</p>
