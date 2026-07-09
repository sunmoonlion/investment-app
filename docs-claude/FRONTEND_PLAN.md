# Research App Frontend Plan

## Decision

`research-app` follows the v4 Agent pairing decision:

```text
research-admin-frontend (Vue 3 + Vite + Element Plus)
  -> research-admin-backend /api/admin/**

research-web-frontend (Next.js)
  -> research-admin-backend /api/agent/** directly
  -> UIEvent + LiveDelta streams

research-web-backend / nodebullworker
  -> not in the M1 Agent critical path
  -> optional M2 BFF only when SSR/SEO, cross-app aggregation, or Node-side auth gateway is justified
```

The reason is that Agent execution, checkpoints, interrupt/resume, event
projection, and SSE all live in the Python/FastAPI/LangGraph runtime. Routing
Agent traffic through Node in M1 would duplicate streaming and reconnect
semantics without adding product value.

## Admin Frontend Scope

Use `research-admin-frontend` only for internal management:

- AgentProfile and runtime configuration management;
- prompt/config review;
- admin-only diagnostics;
- deployment/traffic gate controls;
- operational audit and recovery views.

It should not become the end-user Agent chat/workspace UI.

## Agent Web Frontend Scope

Use `research-web-frontend` for end-user Agent product flows:

- session creation and run start;
- SSE timeline connected to `/api/agent/sessions/{session_id}/stream`;
- persisted UIEvent replay with `last_event_id`;
- LiveDelta typewriter/progress rendering;
- interrupt/resume UX;
- tool cards, files, Markdown preview, and sandbox/VNC viewer;
- user-facing workspace/session navigation once M2 workspace is introduced.

## mooc-manus/ui Absorption

Use old `mooc-manus/ui` as a golden sample for shell and interaction patterns,
not as a data-layer migration.

Absorb:

- Next/React/Tailwind/Radix/shadcn shell style;
- VNC sandbox viewer;
- SSE typewriter timeline;
- tool call cards;
- Markdown/file preview;
- interrupt waiting state.

Rebuild:

- event consumption;
- session/message/state data shapes;
- backend API clients;
- auth and reconnect logic.

Frontend consumes only:

- `UIEvent` for persisted timeline projections;
- `LiveDelta` for disposable live typing/progress updates.

Frontend must not consume raw LangGraph events or old overloaded Event payloads.

## API Boundary Rules

- `research-web-frontend` calls `/api/agent/**` on `research-admin-backend`.
- `research-admin-frontend` calls `/api/admin/**` on `research-admin-backend`.
- End-user tokens must not reach `/api/admin/**`.
- Staff impersonation of an end-user run must be explicit and audited.
- `research-web-backend` is not used for run/start/resume/SSE in M1.

## M1 Acceptance

The first Agent UI slice is complete when `research-web-frontend` can:

1. create an Agent session;
2. start a run;
3. subscribe to SSE;
4. render persisted UIEvents;
5. render LiveDelta separately and reconcile with final UIEvent;
6. resume an interrupt;
7. reconnect with `last_event_id` without duplicate or missing persisted UIEvents.

## Validation

- `research-web-frontend`: run `pnpm typecheck` and `pnpm build`.
- `research-admin-frontend`: run `pnpm type-check` and `pnpm build-only`.
- Backend Agent API changes must keep Phase 0 replay/SSE validation green.
