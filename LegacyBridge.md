# LegacyBridge
## Portable Narrative Continuity Across AI Dungeon Adventures

**Working Draft 0.1 — November 2026**

### Abstract

LegacyBridge proposes a portable continuity system that allows an AI Dungeon adventure to export its important story outcomes as a compact, versioned code that can be imported into another adventure.

Inspired by video-game sequels that recognize earlier save files, LegacyBridge would allow separate scenarios to form a persistent series without requiring access to one another's save data or narrative history.

Its central principle is that **a sequel should inherit established consequences, not merely assume a generic backstory**.

### 1. The Problem: Adventures Without Persistent History

AI Dungeon scenarios typically begin as independent experiences. Even when two adventures share characters and settings, the second adventure cannot reliably know what occurred in the first.

Did the player rescue their companion? Were they imprisoned? Did they betray an organization, establish an alliance, or leave an important conflict unresolved?

Conventional solutions require the player to manually summarize previous events or rely on the AI storyteller to reconstruct history.

Both approaches are vulnerable to omission, ambiguity, and contradiction.

LegacyBridge instead transfers a compact record of mechanically significant narrative facts.

### 2. Proposed Architecture

LegacyBridge consists of four principal operations:

**TRACK:** Record significant story states and confirmed outcomes in persistent JavaScript data.

**INSPECT:** Allow the player to review the continuity information the system currently believes to be true.

**EXPORT:** Encode the relevant information into a portable, copyable sequel code.

**IMPORT:** Decode and validate the code in a compatible scenario, reconstructing the inherited continuity profile.

Proposed player commands include:

- `#SEQUEL STATUS`
- `#SEQUEL EXPORT`
- `#SEQUEL IMPORT <code>`

The export format would contain a schema version, source scenario identifier, continuity data, and an error-detection checksum.

The code would be designed for copy-and-paste portability, not secrecy or cheat prevention.

### 3. Example: SCP: Spellbound to Pandora Protocol

In *SCP: Spellbound*, the player is a modern-day mage whose loved one has been detained by the SCP Foundation.

The adventure permits multiple outcomes: successful rescue, imprisonment, negotiated cooperation, escape, betrayal, or an unresolved confrontation.

LegacyBridge might preserve:

```json
{
  "schema": 1,
  "series": "scp-occult",
  "source": "spellbound",
  "playerStatus": "fugitive",
  "lovedOne": {
    "relationship": "sibling",
    "status": "rescued"
  },
  "foundationRelation": "hostile",
  "site28Status": "damaged",
  "chaosInsurgencyRelation": "contacted"
}
```

This is an illustrative schema, not an implemented export format.

When the player begins *SCP: Pandora Protocol*, they paste their sequel code.

JavaScript validates the code and reconstructs the relevant historical facts.

The scenario then procedurally establishes an opening consistent with those facts.

For example, a fugitive who damaged Site-28 might receive a reluctant, covert Foundation approach. A cooperative spellcaster might be contacted through an established handler. A contained player might receive the offer directly inside their cell.

All three begin the same overarching adventure, but with different circumstances, relationships, and consequences.

### 4. Mechanics, Procedural Generation, and AI Narration

LegacyBridge follows the same hierarchy established in *Mechanically Governed Generative Storytelling*.

**Layer 1 — Authoritative continuity data.** JavaScript establishes which imported historical facts are true.

**Layer 2 — Procedural scenario generation.** Rules select compatible starting conditions, available characters, relationships, and unresolved conflicts.

**Layer 3 — AI storyteller.** The AI converts those conditions into natural dialogue, descriptions, and scenes without contradicting established facts.

**Layer 4 — Player agency.** The player decides how to respond. Imported history determines the situation, not the player's next action.

This distinction is fundamental.

LegacyBridge does not generate a predetermined sequel storyline. It establishes the consequences of the past and allows a new adventure to unfold from them.

### 5. The Challenge of Tracking Narrative Truth

Encoding and decoding continuity data is relatively straightforward.

Determining which events actually occurred is considerably harder.

A player's statement that they intend to rescue someone does not establish a successful rescue. An AI description of an attempted escape does not necessarily establish freedom.

LegacyBridge therefore requires conservative outcome tracking.

Whenever possible, mechanically verified events update continuity directly. Important narrative outcomes can be reported through structured AI-to-JavaScript markers, with validation and duplicate protection.

Ambiguous outcomes should remain unresolved rather than being guessed.

A status-inspection command would let players detect discrepancies before exporting. An optional correction mechanism could permit explicit repairs to the continuity record when the storyteller's actual outcome was missed.

### 6. Supporting an Ongoing Series

LegacyBridge should not be limited to transferring information between two specific scenarios.

A later adventure could inherit continuity from several predecessors.

For example:

**Spellbound → Pandora Protocol → Future SCP Adventure**

The second scenario imports the first scenario's history, adds its own significant outcomes, and exports a new continuity profile.

To prevent codes from growing indefinitely, the system should preserve important inherited facts rather than concatenate entire previous save files.

The design must also distinguish permanent history from current conditions. A past betrayal may remain relevant even after two organizations reconcile.

An export should be available at any point, including during unfinished adventures. A sequel can then recognize unresolved situations rather than inventing an ending.

### 7. Current Development State

LegacyBridge is currently a proposed system, not an implemented library.

The initial use case, portable code approach, core commands, continuity categories, and import-driven procedural openings have been outlined.

The exact serialization format, checksum algorithm, validation rules, state schemas, and cross-scenario compatibility contracts remain to be designed and tested.

The first implementation should be developed alongside *SCP: Spellbound*, so plot-critical events are tracked from the beginning rather than reconstructed after development.

A small independent test harness should verify round-trip serialization, malformed-code rejection, version handling, and consistency across several possible adventure outcomes.

### 8. Relationship to ScriptBridge

LegacyBridge and ScriptBridge solve different problems.

**ScriptBridge provides horizontal interoperability:** independent systems communicate during an adventure.

**LegacyBridge provides longitudinal continuity:** separate adventures exchange meaningful historical information across time.

The two could eventually cooperate. For example, LegacyBridge might export a character's established magical capabilities or psychological history using schemas supplied by Surge Protector or MindRift.

However, importing such information must respect the receiving system's authority and compatibility rules. A continuity record should never silently bypass a game's mechanical restrictions.

### Conclusion

LegacyBridge addresses the problem of **persistent narrative consequences across independent adventures**.

By combining authoritative state tracking, portable export codes, deterministic imports, procedural scenario setup, and AI narration, it offers a practical foundation for connected AI Dungeon campaigns.

**Its governing idea: a player's past should meaningfully shape the next adventure without dictating its future.**
