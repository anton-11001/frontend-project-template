# Project Structure Blueprint

```text
src/
├── api/                         # Global API infrastructure
│   ├── instance.ts              # Axios configuration (base URL, 401/refresh interceptors)
│   ├── endpoints.ts             # ENDPOINTS object — single source of truth for all URLs
│   ├── query-keys.ts            # Constants for TanStack Query (cache keys)
│   └── types.ts                 # Shared API types (e.g., GenericResponse<T>, Pagination)
│
├── router/                      # Navigation configuration
│   ├── paths.ts                 # Route path constants (e.g., PATHS.auth.login)
│   ├── index.tsx                # Main RouterProvider and route definitions
│   └── components/              # Route guards (ProtectedRoute, PublicRoute) and Layouts
│
├── features/                    # BUSINESS LOGIC (Horizontal feature modules)
│   ├── [feature-name]/          # Example: auth, letters, billing
│   │   ├── api/                 # Feature-specific network logic
│   │   │   ├── hooks/           # TanStack Query hooks only (useLogin, useGetLetter)
│   │   │   └── types.ts         # DTOs (Data Transfer Objects) — request/response types
│   │   ├── components/          # Private components used only within this feature
│   │   ├── pages/               # Feature screens (LoginPage, LetterDetailPage)
│   │   ├── store/               # (Optional) Feature-specific state (Zustand/Redux)
│   │   ├── validation/          # Zod schemas for feature forms
│   │   └── index.ts             # Public API (Export only what other modules need)
│
├── components/                  # UI-KIT (Shared Components)
│   ├── ui/                      # Atomic components (Button, Input, Modal, Badge)
│   ├── common/                  # Complex shared elements (AppHeader, Sidebar)
│   └── index.ts
│
├── contexts/                    # Global React Contexts
│   ├── auth-context.tsx         # Session state (user data, isAuth status)
│   └── theme-context.tsx        # UI theme state (light/dark mode)
│
├── hooks/                       # Global reusable React hooks
│   ├── use-debounce.ts
│   ├── use-local-storage.ts
│   └── use-media-query.ts
│
├── utils/                       # Pure utility functions (Helpers)
│   ├── date.ts                  # Date formatting (date-fns/dayjs)
│   ├── mask.ts                  # Input masking (IPs, phones, credit cards)
│   └── storage.ts               # Type-safe wrappers for LocalStorage
│
├── locales/                     # i18n (Internationalization)
│   ├── en/                      # English translations
│   └── ua/                      # Ukrainian translations
│
├── theme/                       # Global styling configuration
│   ├── colors.ts
│   ├── breakpoints.ts
│   └── index.ts                 # Tailwind config or CSS-in-JS theme provider
│
├── types/                       # Global TypeScript declarations
│   └── entity.ts                # Pure domain models/interfaces (User, Letter, Session)
│
├── main.tsx                     # Application entry point
└── App.tsx                      # Root component (Provider tree: QueryClient, Auth, Router)

```

---

## src/

### api/

Global infrastructure for network requests and server state.

* **instance.ts**: Axios configuration including base URL and interceptors for 401 Unauthorized handling and silent token refresh logic.
* **endpoints.ts**: Centralized ENDPOINTS object serving as the single source of truth for all API URLs.
* **query-keys.ts**: Static constants for TanStack Query cache keys to ensure consistent data invalidation.
* **types.ts**: Shared API-specific TypeScript definitions such as GenericResponse and PaginationParams.

### router/

Application navigation and routing logic.

* **paths.ts**: Route path constants used throughout the app (e.g., PATHS.auth.login).
* **index.tsx**: Main RouterProvider setup and route tree definitions.
* **components/**: Route guards including ProtectedRoute for authenticated sessions and PublicRoute for guest access, plus Layout wrappers.

### features/

Business logic organized into horizontal modules. Each subdirectory represents a self-contained domain.

* **[feature-name]/** (e.g., auth, letters, billing)
* **api/**: Network logic specific to this feature.
* **hooks/**: Dedicated TanStack Query hooks (e.g., useLogin, useGetLetter).
* **types.ts**: DTO (Data Transfer Object) definitions for feature-specific requests and responses.


* **components/**: Private components used exclusively within this specific feature.
* **pages/**: Feature-level screens and page components.
* **store/**: Feature-specific state management (Zustand or Redux slices).
* **validation/**: Zod schemas or validation rules for feature forms.
* **index.ts**: Public API for the feature; exports only the components and hooks intended for external use.



### components/

Shared UI-KIT components.

* **ui/**: Atomic, stateless components such as Button, Input, Modal, and Badge.
* **common/**: Complex shared components used across features, such as AppHeader or Sidebar.
* **index.ts**: Central export file for the shared component library.

### contexts/

Global React Context providers.

* **auth-context.tsx**: Global session management containing user data and authentication status.
* **theme-context.tsx**: Global UI state for theme management (light/dark mode).

### hooks/

Global, reusable custom React hooks.

* **use-debounce.ts**
* **use-local-storage.ts**
* **use-media-query.ts**

### utils/

Pure helper functions and utilities.

* **date.ts**: Logic for date manipulation and formatting.
* **mask.ts**: Input masking utilities for IPs, phone numbers, or sensitive data.
* **storage.ts**: Type-safe wrappers for browser storage interaction.

### locales/

Internationalization and translation assets.

* **en/**: English translation files.
* **ua/**: Ukrainian translation files.

### theme/

Global styling configuration and design system tokens.

* **colors.ts**
* **breakpoints.ts**
* **index.ts**: Integration for Tailwind configuration or CSS-in-JS theme providers.

### types/

Global TypeScript declarations for domain models.

* **entity.ts**: Pure domain interfaces (e.g., User, Letter, Session) representing the business logic, independent of API structures.

### Entry Files

* **main.tsx**: Application entry point for the build tool.
* **App.tsx**: Root component containing the Provider tree (QueryClientProvider, AuthProvider, RouterProvider).
