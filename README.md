# frontend-project-template
Universal Frontend Project Template

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
