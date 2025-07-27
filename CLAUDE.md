# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Context: Faithful Archive

This is **Faithful Archive**, a fork of ArDrive Web being transformed into a dedicated platform for uploading and sharing Christ-honoring spiritual content on Arweave. The project aims to ensure sermons, worship resources, and Bible studies remain permanently accessible.

### Key Transformation Goals
- **Strip ~80% of ArDrive features** to create a lean, purpose-built MVP
- **Retain only**: Arweave wallet auth, topping-up mechanisms, upload strategies, and encryption
- **Add new features**: Content moderation queue, spiritual metadata, and curated browsing
- **Focus**: Spiritual archive for pastors, worship leaders, and Bible teachers

See PRD.md for full project details and roadmap.

## Essential Commands

### Setup & Development
```bash
# Initial setup (clean install and code generation)
scr setup

# Start watching for code generation changes
flutter packages pub run build_runner watch

# Run the web app in development mode
flutter run -d chrome --dart-define=environment=development

# Run the web app in production mode
flutter run -d chrome --dart-define=environment=production

# Run on mobile devices
flutter run --flavor=development  # or --flavor=production
```

### Testing & Quality
```bash
# Run all tests (main app and packages)
scr test

# Run tests for specific package
cd packages/[package_name] && flutter test

# Analyze code
flutter analyze

# Check database schema
scr check-db

# Verify Flutter version
scr check-flutter
```

### Build & Code Generation
```bash
# One-time code generation (when switching branches or after model changes)
flutter pub run build_runner build --delete-conflicting-outputs

# Generate code for packages/ario_sdk specifically
cd packages/ario_sdk && flutter pub run build_runner build --delete-conflicting-outputs
```

## Architecture Overview

### Core Architecture Pattern
- **State Management**: BLoC pattern with flutter_bloc
- **Database**: Drift (SQLite) for local storage
- **Code Generation**: Used for JSON serialization, database models, and GraphQL queries
- **Dependency Injection**: Service locator pattern with singleton services

### Key Architectural Components

1. **BLoCs** (`lib/blocs/`): Business logic components that manage state
   - Each major feature has its own BLoC
   - Events trigger state changes
   - UI components consume states via BlocBuilder/BlocListener

2. **Services** (`lib/services/`): External integrations
   - `ArweaveService`: Blockchain interactions
   - `ArDriveUploadManager`: File upload orchestration
   - `ArConnectService`: Wallet integration
   - `TurboPaymentService`: Payment processing

3. **Core** (`lib/core/`): Fundamental functionality
   - `ArDriveCrypto`: Encryption/decryption
   - `ArFS`: Arweave File System implementation
   - Upload pipeline with resumable uploads

4. **Database** (`lib/models/`):
   - Drift database with DAOs for drives, files, transactions
   - Schema migrations handled via drift_schemas
   - Database validation through check-db script

### Important Development Patterns

1. **Code Generation Required For**:
   - Database models (`.drift` files)
   - JSON serialization (`@JsonSerializable`)
   - GraphQL queries (Artemis in `lib/services/arweave/graphql/`)

2. **Multi-Package Structure**:
   - Local packages in `packages/` directory
   - Each package has its own pubspec.yaml and tests
   - Shared functionality extracted to packages

3. **Environment Configuration**:
   - Three flavors: development, staging, production
   - Configuration via `--dart-define` for web
   - `--flavor` flag for mobile builds

### Git Commit Conventions
Prefix commits with:
- `fix:` bug fixes
- `feat:` new features
- `perf:` performance improvements
- `docs:` documentation changes
- `style:` formatting changes
- `refactor:` code refactoring
- `test:` adding tests
- `chore:` maintenance tasks

Use lowercase for commit messages.

### Testing Strategy
- Unit tests for business logic (BLoCs, services)
- Widget tests for UI components
- Integration tests for critical user flows
- All packages must have their own test suites
- Tests must pass before merging to dev

### Deployment Flow
- `dev` branch → staging deployment (TBD - will be set up for Faithful Archive)
- `master` branch → production deployment (TBD - will be set up for Faithful Archive)
- PR previews available for all PRs to dev
- Note: Currently inherits ArDrive's deployment config - needs updating for Faithful Archive