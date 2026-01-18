✅ 1 what do you use to keep the repo clean ?
* Husky Git hooks (.husky/pre-commit, .husky/commit-msg)
* es lint 9

✅ 2 what is the folder structure ?
* app/ src/api/ ...

✅ 3 how is the routing and providers handled ?
* Root layout: app/_layout.tsx = app-level providers
* Tabs layout: app/(tabs)/_layout.tsx = navigation config
* Routes are files → predictable scaling
* “Providers live at the root layout so hooks are usable everywhere, including nested routes.”

✅ 4 what is ts aliasing, module aliasing runtime aliasing ?
* TS alias: tsconfig.json → @/* -> src/*
* Babel alias: babel.config.js using module-resolver

✅ 5 how are central http client and interceptors handling everything ?
* axios.create(), interceptor adds timezone header, 
* Global auth token injection hook (setAuthToken())
* “All request policies live in one place: auth headers, timeouts, retries, error normalization.”

✅ 6 Service layer (domain boundary) **
* velib.service.ts is the only place that knows: endpoint URL / query params / refine
* GeoJSON parsing station normalization logic

“Service layer isolates API details and keeps UI stable if backend changes.”

✅ 7 Runtime data validation (Zod) = enterprise-grade robustness  **

* Zod schemas validate API responses at runtime
* Convert untrusted JSON → safe, structured types
* Prevents silent crashes when fields change

* “TypeScript doesn’t protect you from runtime API changes — Zod does.”

✅ 8 Normalization: raw API → stable domain model

* normalizeStation() turns inconsistent API fields into a clean model:
* id, name, lat, lng, bikes, ebikes, docks
* multiple fallback mappings (stationcode, station_id, etc.)

* “We normalize external data once, so the UI always consumes predictable types.”

✅ 9 React Query as the data layer (beyond useEffect)

* useVelibStations() = canonical data access hook
* queryKey design
* caching (staleTime, gcTime) retry strategy
* consistent loading/error state patterns

* “Server state belongs in React Query, not in local useState/useEffect.”

✅ 10 Search filtering via memoization (performance awareness) ? also whats memoisation ?
* On List screen:
* local state: q
* derived list: useMemo() filtering
* avoids recomputing on every render unnecessarily

* “Derived state should be computed predictably and efficiently.”


✅ 11 Multi-context state layering ?

* all in app/_layout.tsx
* AuthContext (token wiring)
* ConfigContext (timezone/appName)
* FeatureFlagsContext (future toggles)
* ThemeProvider (design tokens & mode)

* “Separate contexts by domain instead of one global god-store.”


✅ 12 Design tokens + ThemeProvider (RN equivalent of SCSS + MUI theme) ?

* theme.ts defines tokens: colors spacing radius
* provider controls light/dark
* scalable: you can add typography, shadows, etc.