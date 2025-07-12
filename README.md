# WrapSync

**WrapSync** is an event-driven integration that captures agent wrap-up data from Genesys Cloud and synchronizes it with the core banking system in near real-time.

## 🚀 Overview

Agents often skip wrap-up entries in Genesys to avoid double entry in the core. WrapSync solves this by capturing key interaction metadata and wrap-up notes at the end of an interaction and pushing them to the core system via a secure REST API.

## 🧩 Architecture

### Components
- **Genesys Architect Workflow**: Triggers on `Interaction Disconnected` event.
- **Genesys Web Action**: Formats data and calls the Azure Function.
- **Azure Function API (Python)**: Accepts JSON payload and updates the core system.
- **Genesys Data Tables**: Stores failed syncs for retries.

### Data Flow
```
Wrap-up complete → Interaction Disconnected Event →
Architect Workflow → Web Action → Azure Function →
Core Banking System + Agent Notification
```

## 📦 Key Features
- Sync wrap-up code and notes, agent info, interaction ID, and more.
- Reliable retry logic with exponential backoff (1s, 5s, 15s).
- Genesys Data Table dead letter queue for manual recovery.
- Admin retry workflow and configurable logging.
- Real-time sync notifications to agents.

## 🛡️ Design Priorities
- **Reliability First**: Graceful degradation during core/API downtime.
- **Real-Time Sync**: Sub-30s delay after interaction end.
- **Genesys-Native**: Minimal external dependencies.
- **Admin Visibility**: Clear tracking, diagnostics, and retries.

## 📈 Future Roadmap
- Historical bulk sync
- Status dashboard
- Cross-system integration
- Enhanced analytics

## 📝 License
Internal TTCU use only. For questions or enhancements, contact the Technology & Innovation team.
