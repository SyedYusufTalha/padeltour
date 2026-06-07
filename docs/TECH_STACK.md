# Tech Stack

## Decision Summary

| Layer | Choice | Reason |
|-------|--------|--------|
| Mobile framework | Flutter (Dart) | Single codebase for iOS + Android, native performance, no subscription |
| Database | Firebase Firestore | Free Spark plan, real-time sync, perfect for live tournament scoring |
| Authentication | Firebase Auth | Free, supports email/password, Google, Apple Sign-In |
| File storage | Firebase Storage | Free 5 GB, used for profile pictures and assets |
| State management | Riverpod | Type-safe, testable, scales cleanly with clean architecture |
| Navigation | go_router | Declarative routing, deep linking, Flutter team recommended |
| Models | Freezed + json_serializable | Immutable data classes, automatic JSON serialisation |
| Linting | very_good_analysis | Strict lint rules, enforces best practices |
| CI/CD | GitHub Actions | Free for public repos, runs tests + builds on push |

---

## Flutter

**Version policy**: always use the latest stable channel (`flutter channel stable`).

Flutter compiles Dart to native ARM code — there is no JavaScript bridge. This means:
- Pixel-perfect UI on both Android and iOS from a single codebase.
- 60/120 fps rendering via the Impeller engine.
- A single `pubspec.yaml` manages all dependencies.

---

## Firebase (free Spark plan)

No credit card is required on the Spark plan. Limits that matter for early development:

| Resource | Free Limit |
|----------|-----------|
| Firestore reads | 50,000 / day |
| Firestore writes | 20,000 / day |
| Firestore deletes | 20,000 / day |
| Firestore storage | 1 GiB |
| Auth users | Unlimited |
| Cloud Storage | 5 GiB |
| Hosting bandwidth | 10 GiB / month |

When limits are approached, the app will be upgraded to the Blaze (pay-as-you-go) plan — still essentially free at low usage.

### Why Firestore for tournaments?
Firestore's **real-time listeners** push score updates to all connected devices instantly. This means:
- A court-side scorer updates a match result.
- All participants' phones update the leaderboard in real time — no manual refresh.

---

## Architecture: Clean Architecture (Feature-First)

The app follows **Clean Architecture** split into three layers, organised by feature:

```
lib/
├── core/                    # Shared utilities, constants, theme, routing
│   ├── constants/
│   ├── errors/
│   ├── router/
│   └── theme/
├── features/
│   ├── auth/
│   │   ├── data/            # Firebase Auth calls, DTOs
│   │   ├── domain/          # Entities, repository interfaces, use cases
│   │   └── presentation/    # Riverpod providers, screens, widgets
│   ├── tournament/
│   │   ├── data/
│   │   ├── domain/
│   │   └── presentation/
│   └── player/
│       ├── data/
│       ├── domain/
│       └── presentation/
└── main.dart
```

### Layer responsibilities

| Layer | Responsibility | May depend on |
|-------|---------------|---------------|
| `data` | Firebase queries, DTOs, repository implementations | Firebase SDK |
| `domain` | Entities, repository interfaces, pure business logic | Nothing (no Flutter, no Firebase) |
| `presentation` | UI widgets, Riverpod providers | `domain` only |

This separation means:
- Business logic (tournament scoring algorithms) can be unit-tested without Firebase or Flutter.
- Swapping Firebase for a different backend only touches the `data` layer.

---

## State Management: Riverpod

Riverpod providers act as the bridge between the `domain` and `presentation` layers.

```
UI Widget
    └── watches Provider
            └── calls Use Case (domain)
                    └── calls Repository Interface (domain)
                            └── implemented by Repository (data)
                                    └── calls Firebase SDK
```

---

## Key Packages

```yaml
dependencies:
  # Firebase
  firebase_core: ^latest
  firebase_auth: ^latest
  cloud_firestore: ^latest
  firebase_storage: ^latest

  # State management
  flutter_riverpod: ^latest
  riverpod_annotation: ^latest

  # Navigation
  go_router: ^latest

  # Models
  freezed_annotation: ^latest
  json_annotation: ^latest

  # UI utilities
  flutter_svg: ^latest
  cached_network_image: ^latest

dev_dependencies:
  # Code generation
  build_runner: ^latest
  freezed: ^latest
  json_serializable: ^latest
  riverpod_generator: ^latest

  # Linting
  very_good_analysis: ^latest

  # Testing
  flutter_test:
    sdk: flutter
  mocktail: ^latest
```

---

## Code Quality Standards

### Linting
`very_good_analysis` is the strictest Flutter lint ruleset. It enforces:
- Always declare return types
- Prefer `const` constructors
- No unused imports
- Trailing commas for better diffs

### Formatting
`dart format` is run automatically. Line length: **80 characters**.

### Git workflow
- Branch naming: `feature/`, `fix/`, `docs/`
- Commit messages: conventional commits (`feat:`, `fix:`, `docs:`, `refactor:`)
- PRs require passing CI before merge

### Testing requirements
| Test type | Coverage target | Tool |
|-----------|----------------|------|
| Unit (domain logic) | All use cases + scoring algorithms | `flutter_test` + `mocktail` |
| Widget | Key screens | `flutter_test` |
| Integration | Core user flows | `integration_test` |

### CI/CD (GitHub Actions — free)
On every push to `main` and every PR:
1. `dart format --set-exit-if-changed` — fail if code is unformatted
2. `flutter analyze` — fail on any lint warning
3. `flutter test` — fail on any test failure
4. `flutter build apk --debug` — verify Android builds
5. `flutter build ios --no-codesign` — verify iOS builds (on macOS runner)

---

## Documentation Convention

Every feature added to the app gets a corresponding doc file in `docs/features/`:

```
docs/
├── TOURNAMENT_FORMATS.md      # Play styles reference (this exists)
├── TECH_STACK.md              # This file
├── ARCHITECTURE.md            # Detailed data model + Firestore schema
└── features/
    ├── auth.md                # Auth flow, screens, Firebase rules
    ├── tournament_create.md   # Create tournament flow
    ├── tournament_scoring.md  # Live scoring, round generation
    └── ...
```

Each feature doc covers: purpose, user flows, data model, Firestore collections, and edge cases.
