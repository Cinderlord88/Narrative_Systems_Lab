# ScriptBridge
## A Standardized Interoperability Protocol for AI Dungeon JavaScript Systems

**Working Draft 0.1 — November 2026**

### Abstract

ScriptBridge proposes a lightweight, standardized communication protocol allowing independently developed AI Dungeon JavaScript systems to exchange information and request services without requiring custom integration code for every combination of scripts.

Its central principle is simple: **scripts should communicate through capabilities and agreed-upon interfaces, rather than through hard-coded knowledge of one another.**

A supernatural ability engine, psychological simulation, combat system, and relationship engine should be able to cooperate while remaining independently usable.

### 1. The Problem: Isolated Systems

AI Dungeon scripting projects increasingly model distinct aspects of a simulated world.

Surge Protector governs supernatural abilities. MindRift models psychological conditions. Other systems manage combat, exploration, relationships, or narrative events.

These systems may need information from one another. A failed magical ritual could trigger psychological stress. A combat injury might affect a character's ability to perform a spell. A relationship engine might react to a witnessed betrayal.

Without a common protocol, every new script requires special-purpose integrations with existing scripts. As the number of systems increases, this creates an increasingly difficult maintenance problem.

ScriptBridge aims to eliminate that dependency.

### 2. Proposed Architecture

ScriptBridge uses a compact, REST-inspired interface implemented through ordinary JavaScript function calls and structured messages, not an actual HTTP server.

Four general operations form the foundation:

- **DISCOVER:** Identify available capabilities and their versions.
- **QUERY:** Retrieve information from a system that owns it.
- **COMMAND:** Request that an authoritative system perform an operation.
- **EVENT:** Announce that something significant has occurred.

Scripts advertise capabilities such as `magic.registry`, `psychology.stress`, or `combat.damage`, rather than requiring callers to know specific script names.

A standardized envelope identifies the operation, capability, payload, protocol version, and optional event or request ID.

The receiving system validates the message and either handles it or returns an appropriate response.

### 3. Example: Magic and Psychological Stress

Imagine a character attempts a forbidden magical ritual.

Surge Protector evaluates the attempted supernatural effect against the character's registered abilities.

The ritual succeeds, but the experience exposes the character to an incomprehensible entity.

The responsible system emits an event conceptually equivalent to:

```json
{
  "protocol": "ScriptBridge/1",
  "operation": "EVENT",
  "capability": "psychology.stress",
  "event": "eldritch_exposure",
  "eventId": "scene42-exposure1",
  "payload": {
    "character": "Player",
    "severity": "major",
    "cause": "forbidden_ritual"
  }
}
```

MindRift, if installed and subscribed to the relevant event, determines the psychological consequences using its own rules.

Surge Protector does not calculate Stress. MindRift does not decide whether the spell was permitted.

**Each system remains authoritative over its own mechanics.**

The AI storyteller then receives the verified results and incorporates them into the narrative.

### 4. Core Design Principles

**Independent operation.** Every participating script must remain functional when other systems are absent.

**Capability-based discovery.** New scripts should be able to offer compatible services without requiring modifications to existing consumers.

**Single mechanical authority.** A mechanic must have one authoritative owner. Other systems may request or observe its results but should not independently overwrite them.

**Versioned contracts.** Messages, capabilities, and schemas must be documented and compatible across releases.

**Graceful degradation.** Unsupported operations and missing providers should not crash unrelated systems.

**Idempotency.** Event identifiers and deduplication should prevent accidental repeated consequences, particularly during AI Dungeon retries.

**Minimal overhead.** The protocol must respect AI Dungeon's execution environment, persistence constraints, and limited narrative context budget.

### 5. Integration with Mechanically Governed Storytelling

ScriptBridge operates primarily beneath the narrative layer:

**Player action → authoritative JavaScript systems → ScriptBridge communication → verified mechanical outcomes → procedural narrative guidance → AI storytelling.**

The protocol coordinates mechanics. It does not give the AI authority to invent or modify mechanical state.

Scripts should also provide a compact, versioned **API Advertisement** near the top of their Library code, identifying implemented capabilities, operations, and integration requirements.

### 6. Current Development State

ScriptBridge is currently an architectural proposal.

Its intended operations, capability discovery model, message contracts, and authority boundaries have been outlined. Existing projects already demonstrate local JavaScript functions, persistent state, commands, and structured narrative events.

However, a shared cross-script discovery registry, standardized message dispatcher, subscription system, and validated inter-script communication have **not yet been established as a working implementation**.

The next milestone is a small reference implementation using two independent systems, ideally Surge Protector and MindRift, supported by automated compatibility and failure-handling tests.

### 7. Future Applications

ScriptBridge could support a modular ecosystem of reusable AI Dungeon components: supernatural abilities, combat, psychology, relationships, inventory, exploration, and procedural world simulation.

The long-term objective is not a monolithic game engine, but a collection of small, understandable systems that can cooperate through a stable common language.

### Conclusion

ScriptBridge addresses the problem of **mechanical interoperability**.

By standardizing how scripts discover capabilities, request operations, and publish events, it offers a path toward increasingly sophisticated simulations without sacrificing modularity, maintainability, or mechanical authority.

**Its governing idea: independent systems should cooperate without becoming dependent on one another's internal implementation.**
