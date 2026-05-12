# Project Structure Blueprint

## src/

### api/

Global infrastructure for network requests and server state.

- **endpoints.ts**: Centralized ENDPOINTS object serving as the single source of truth for all API URLs.

### lib/

Third-party library configurations.

**axios/** folder. Centralized API client configuration and network logic.

- **instance.ts**: Axios configuration including base URL, auth headers, interceptors, 401 Unauthorized handling, and silent token refresh logic.

- **interceptors/**: Separated request/response interceptor logic.

- **types.ts**: Axios-specific internal typings.

**tanstack-query/** folder. Server state management and caching configuration.

- **query-client.ts**: Global TanStack Query client configuration.

- **query-keys.ts**: Static constants for TanStack Query cache keys to ensure consistent data invalidation.

- **types.ts**: Shared TanStack Query utility typings.

### router/

Application navigation and routing logic.

- **paths.ts**: Route path constants used throughout the app (e.g., PATHS.auth.login).
- **index.tsx**: Main RouterProvider setup and route tree definitions.
- **components/**: Route guards including ProtectedRoute for authenticated sessions and PublicRoute for guest access, plus Layout wrappers.

### features/

Business logic organized into horizontal modules. Each subdirectory represents a self-contained domain.

- **[feature-name]/** (e.g., auth, billing)
- **api/**: Pure Axios or Fetch functions (e.g., getProfile, updateBilling) plus a file with type definitions for feature-specific requests and responses.
- **types/**: Feature-local UI or internal types.
- **constants/**: Domain-specific configuration.
- **hooks/**: React hooks.
- **services/**: Sometimes you have complex logic that isn't a Hook or a Component. Local utility functions (e.g., formatCurrencyForBilling, calculateAuthStrength).
- **queries/**: TanStack Query hooks.
- **components/**: Private components used exclusively within this specific feature.
- **pages/**: Feature-level screens and page components.
- **validation/**: Zod schemas or validation rules for feature forms.
- **index.tsx**: It acts as a gatekeeper. You export only what the rest of the app is allowed to see.

### components/

Shared UI-KIT components. Complex shared components used across features, such as AppHeader or Sidebar.

### contexts/

Global React Context providers.

### hooks/

Global, reusable custom React hooks.

### utils/

Pure helper functions and utilities.

### theme/

Global styling configuration and design system tokens. (colors, breakpoints or Tailwind configuration etc.)

### types/

Global TypeScript declarations for domain models.

### **constants.tsx**:

For things like APP_TITLE, SUPPORT_EMAIL, or global pagination defaults that aren't specific to a feature.

### errors/

Centralized application error handling.

- **api-error.ts**: API error normalization.
- **error-codes.ts**: Shared application error codes.
- **handlers/**: Global error handling utilities.
- **boundaries/**: React Error Boundaries.

### Entry Files

- **main.tsx**: Application entry point for the build tool.
- **App.tsx**: Root component containing the Provider tree (QueryClientProvider, AuthProvider, RouterProvider).

## Optional Folders

Additional folders that may be introduced depending on project complexity, architecture, or business requirements.

### locales/

Internationalization and translation assets.

### ui/

Atomic, stateless components such as Button, Input, Modal, and Badge.

### assets/

For SVGs, images, and fonts.

### test/

Dedicated space for ensuring your application behaves as expected.

### store/

Used for Zustand or Redux to handle complex client-side state (like a multi-step form or a persistent sidebar state).

### permissions/

Authorization and role-based access control logic.

- **roles.ts**: System roles and permission maps.
- **guards/**: Permission validation helpers.
- **hooks/**: Hooks like usePermissions or useRoleAccess.

### config/

Application-wide static configuration.

- **app.ts**: General app configuration.
- **feature-flags.ts**: Runtime feature toggles.
- **navigation.ts**: Sidebar or menu configuration.
- **client.ts**: Safe client-side environment variables.
- **server.ts**: Server-only environment variables if applicable.

## Conventions

- Prefer feature-first architecture.
- Avoid cross-feature imports when possible.
- Shared logic must live in shared layers only.
- Components should remain presentation-focused.
- TanStack Query handles server state.
- Zustand/Redux handles client state only.
- Avoid direct API calls inside components.
- Prefer composition over inheritance.
- Prefer explicit exports through feature `index.ts`.
- Keep business logic outside JSX.

## Import Rules

Dependency direction should remain predictable.

Allowed flow:

```txt
app → pages → features → shared
```

Disallowed:

- features importing from other unrelated features
- shared importing from features
- components directly calling APIs
