# MemoryVault

## Overview

MemoryVault is an AI memory layer application that organizes conversation history into "memory chains" instead of raw chats. It provides a visual interface for managing long-term memory for AI agents, featuring a three-tier memory system (Hot/Warm/Cold), real-time WebSocket updates, and integration capabilities with external memory services like Supermemory.ai.

The application solves conversation fragmentation by grouping related conversations based on intent and repeated concepts, allowing users to search, visualize, and resume thinking flows.

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

### Frontend Architecture
- **Framework**: React 18 with TypeScript, bundled via Vite
- **Routing**: Wouter for lightweight client-side routing
- **State Management**: TanStack React Query for server state and caching
- **Styling**: Tailwind CSS with shadcn/ui component library (New York style)
- **Animations**: Framer Motion for smooth transitions
- **Real-time**: WebSocket client for live view updates

The frontend follows a pages-based structure with reusable components. Key pages include Landing (marketing), Dashboard (memory chain management), and Chat (AI conversation interface).

### Backend Architecture
- **Framework**: Express.js with TypeScript
- **API Pattern**: RESTful endpoints defined in shared route schemas with Zod validation
- **Real-time**: WebSocket server (ws library) for broadcasting view updates
- **Storage**: In-memory storage class with PostgreSQL-ready Drizzle ORM schema
- **Build**: Custom esbuild script for production bundling

The backend uses a storage abstraction layer (`IStorage` interface) that currently implements in-memory storage but is designed for easy PostgreSQL migration.

### Data Model
- **Chains**: Memory chains with title, summary, keywords (hot memory tokens), and Supermemory document linking
- **Cards**: Individual prompts within chains, ordered sequentially
- **Memory Context**: Three-tier structure (hot/warm/cold) for memory retrieval

### Shared Code
The `shared/` directory contains:
- Database schema definitions (Drizzle ORM)
- API route contracts with Zod schemas
- TypeScript types shared between client and server

## External Dependencies

### Database
- **PostgreSQL**: Primary database via Drizzle ORM (requires `DATABASE_URL` environment variable)
- **Drizzle Kit**: Database migrations and schema pushing

### Third-Party Services
- **Supermemory.ai**: External memory API integration for AI memory storage and retrieval (requires `SUPERMEMORY_API_KEY`)
- **OpenAI**: AI capabilities for chat functionality (requires `OPENAI_API_KEY`)

### Key npm Packages
- `drizzle-orm` / `drizzle-zod`: Database ORM and schema validation
- `@tanstack/react-query`: Data fetching and caching
- `framer-motion`: Animation library
- `ws`: WebSocket server implementation
- `zod`: Runtime type validation
- Full shadcn/ui component set via Radix primitives

### Development Tools
- Replit-specific Vite plugins for development experience
- TypeScript with strict mode
- PostCSS with Tailwind and Autoprefixer