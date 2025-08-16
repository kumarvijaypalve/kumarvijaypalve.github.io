# Overview

SecureChat is an anonymous encrypted messaging web application that enables users to create temporary chat rooms with end-to-end encryption. Users can generate room codes, share them with others, and engage in secure conversations without requiring user accounts or personal information. The application emphasizes privacy and security through client-side encryption using room codes as encryption keys.

# User Preferences

Preferred communication style: Simple, everyday language.

# System Architecture

## Frontend Architecture

The client-side is built with **React 18** and **TypeScript**, using a modern component-based architecture:

- **UI Framework**: Utilizes shadcn/ui components built on Radix UI primitives for consistent, accessible design
- **Styling**: Tailwind CSS with custom design tokens for theming and responsive design
- **State Management**: React Query (@tanstack/react-query) for server state management and caching
- **Routing**: Wouter for lightweight client-side routing
- **Real-time Communication**: WebSocket integration for live messaging
- **Build Tool**: Vite for fast development and optimized production builds

The application follows a feature-based component structure with reusable UI components, custom hooks for WebSocket management, and utility functions for encryption/decryption operations.

## Backend Architecture

The server-side uses **Node.js** with **Express.js** in a minimal REST + WebSocket architecture:

- **API Layer**: Express.js REST endpoints for room creation and joining
- **Real-time Layer**: WebSocket server for live message broadcasting
- **Database Layer**: Drizzle ORM with PostgreSQL support (configured for Neon Database)
- **Session Management**: In-memory storage with fallback to database persistence
- **Security**: Cryptographically secure room code generation using Node.js crypto module

The backend implements a dual storage strategy with in-memory operations for performance and database persistence for reliability.

## Data Storage Solutions

**Database**: PostgreSQL with Drizzle ORM providing type-safe database operations:

- **Schema Design**: Three main entities - rooms, messages, and participants
- **Room Management**: Unique room codes with activity tracking and automatic cleanup
- **Message Storage**: Encrypted content storage with sender information and timestamps
- **Participant Tracking**: Active user management with join/leave events

**In-Memory Storage**: MemStorage class providing fast access for active sessions and real-time operations.

## Authentication and Authorization

The application implements a **sessionless, anonymous architecture**:

- **No User Accounts**: Users are identified only by nicknames within room sessions
- **Room-based Access**: Access control through room codes rather than user authentication
- **Temporary Sessions**: Participant data is cleaned up when users leave or rooms become inactive
- **Encryption Keys**: Room codes serve as both access tokens and encryption keys

## External Dependencies

**Database Services**:
- Neon Database (PostgreSQL hosting)
- Connection pooling via @neondatabase/serverless

**Client-side Libraries**:
- Radix UI primitives for accessible component foundation
- crypto-js for client-side AES encryption/decryption
- date-fns for date formatting and manipulation
- Lucide React for consistent iconography

**Development Tools**:
- TypeScript for type safety across the full stack
- ESBuild for server-side bundling and production builds
- Drizzle Kit for database migrations and schema management

**UI and Styling**:
- Tailwind CSS for utility-first styling approach
- class-variance-authority for component variant management
- Custom CSS variables for consistent theming

The application is designed to be easily deployable on platforms like Replit with minimal configuration, requiring only a DATABASE_URL environment variable for PostgreSQL connectivity.