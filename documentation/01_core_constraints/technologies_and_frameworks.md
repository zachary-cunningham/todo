# Technologies and Frameworks

**Status:** AI-generated | Approved merge to `01_core_constraints/`

**Purpose:** Define the immutable technology stack for this local-first todo application. These decisions cannot be changed without refactoring the entire codebase.

---

## Core Stack

### Frontend Framework
- **React Native** with **Expo** managed workflow
- Enables cross-platform development (iOS, Android) from single codebase
- Expo provides managed build pipeline and native API access

### Programming Language
- **TypeScript** (strict mode)
- Type safety for data models, component props, and local storage interactions
- Prevents runtime errors from data shape mismatches

### UI Framework
- **React** (via React Native)
- Component-based architecture for reusable UI elements
- Gesture Responder system for swipe interactions

---

## Data Layer

### Storage
- **Local storage only** — No backend server or cloud database
- **Expo SecureStore** for sensitive data (if needed in future)
- **AsyncStorage** for todo items, profiles, and app state
- Data persists on device, isolated per installation

### Data Format
- JSON serialization for storage
- All dates stored as ISO 8601 strings
- Arrays for tags and profiles

---

## Key Dependencies

### Required
- `expo` - Managed workflow and native APIs
- `react-native` - Core framework
- `react-native-gesture-handler` - Swipe gestures (left/right)
- `@react-native-async-storage/async-storage` - Persistent local storage

### Phase 2 (Natural Language Processing)
- TBD: Date/time parsing library (e.g., `chrono-node`, `dayjs` with plugins)
- TBD: Text analysis for hashtag extraction

---

## Architectural Constraints

### No Backend
- **No API calls** to external servers for CRUD operations
- **No authentication** required (local device only)
- **No sync** between devices (single-device storage)
- Simplifies architecture: eliminates network error handling, loading states, API versioning

### Platform Targets
- **iOS** (iPhone, iPad via Expo)
- **Android** (phones, tablets via Expo)
- **No web version** (React Native-specific APIs used)

### Development Workflow
- Expo Go for development/testing
- EAS Build for production builds (if deployed)
- TypeScript compiler for type checking pre-runtime

---

## Immutable Decisions

These choices are **core constraints** and cannot be changed without major refactoring:

1. ✓ Local storage only (no backend migration path)
2. ✓ React Native + Expo (cannot switch to native Swift/Kotlin without rewrite)
3. ✓ TypeScript (removing types would break data safety guarantees)
4. ✓ Gesture-based interactions (core to UX, tightly coupled to React Native APIs)

---

## Explicitly Out of Scope

- Server-side rendering
- Database servers (PostgreSQL, MongoDB, etc.)
- API layer (REST, GraphQL)
- User authentication systems
- Multi-device sync
- Web browser compatibility
- Native iOS/Android codebases
