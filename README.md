# ChaOS — Character Operating System for LLMs

ChaOS is a modular, text-native character “operating system” for LLM roleplay that stabilizes long-horizon character continuity and player-style agency using a governance constitution (OTTC: On‑The‑Top Constraint).

This repo is intentionally mostly `.txt` files: the system is designed to be readable, diffable, and runnable inside language itself.

---

## What problem this solves

Long-running LLM “characters” tend to fail in predictable ways:
- drift: identity and commitments melt over time
- thrash: multiple subsystems rewrite the same state in the same turn
- overclaiming: narration / omniscience / asserting outcomes without evidence
- uninspectable behavior: no receipts for why state changed
- brittle tool behavior (if tools exist): tool calls not causally tied to stabilized intent

ChaOS addresses this by treating state updates as governed, auditable deltas.

---

## Start here (5 core files)

If you only read five files, read these in order:

1) `S_STATE_GOVERNANCE_OVERLAY.txt`  
   The non-negotiable write contract (propose → commit), injection defense, and step-limit philosophy.

2) `S_CANONICAL_TOKEN_DICTIONARY.txt`  
   The canonical bracket-path “address space” for state. This is the internal API.

3) `S_COGNITIVE_SCRATCHPAD.txt`  
   Cycle-local workspace (volatile). All COTs write proposals/impulses here.

4) `S_STATE_GOVERNANCE_AND_COMMIT.txt`  
   The single-writer reconciler: canonicalization, conflict resolution, invariants, and commit.

5) `COT_UPDATE_VERIFICATION.txt`  
   Post-commit validator (trace-only). Ensures audit coverage, caps, and integrity checks.

---

## The runtime cycle (high level)

One “turn” / “cycle” is:

1. Instantiate `COGNITIVE_SCRATCHPAD` (volatile workspace).
2. Run COTs in the order defined by `S_UPDATE_CASCADE_REGISTRY.txt`.
3. COTs append:
   - impulses → `[COGNITIVE_SCRATCHPAD][ACTIVE_IMPULSE_REGISTRY]`
   - proposed state deltas → `[COGNITIVE_SCRATCHPAD][PROPOSED_UPDATES_REGISTRY]`
4. `COT_DECISION_SYNTHESIS` selects exactly one action for the cycle.
5. `S_STATE_GOVERNANCE_AND_COMMIT` reconciles proposals and commits the final update set.
6. `COT_UPDATE_VERIFICATION` performs deterministic checks and writes trace output only.
7. Scratchpad is wiped.

---

## File map (how to navigate)

### Governance spine (OTTC / “law”)
- `S_STATE_GOVERNANCE_OVERLAY.txt`
- `S_STATE_GOVERNANCE_AND_COMMIT.txt`
- `S_CANONICAL_TOKEN_DICTIONARY.txt`
- `S_COGNITIVE_SCRATCHPAD.txt`
- `S_UPDATE_CASCADE_REGISTRY.txt`
- `S_TEMPORARY_MODIFIERS.txt`
- `S_LLM_FORMATTING_GUIDELINES_TEMPLATE.txt`

### Persistent character state (diegetic state)
- `PHYSICAL_BODY.txt` (module root: BODY)
- `C_SKILLS.txt` (SKILLS)
- `C_RELATIONAL.txt` (RELATIONAL)
- `C_MEMORY.txt` (MEMORY)
- `C_ALTERATIONS.txt` (ALTERATIONS)
- `C_COPE_STATE.txt` (COPE)
- `DOMINANT_PREDICTIVE_FRAME.txt` (DOMINANT_PREDICTIVE_FRAME)
- `M_GOALS_MOTIVATIONS.txt`, `M_BELIEF_SYSTEMS.txt`, `M_COMMUNICATION_DIALOGUE.txt`

### Cognitive processes (COT modules)
- `COT_SPATIAL_EMBODIMENT_PROCESSING.txt`
- `COT_TEMPORAL_FLOW_PROCESSING.txt`
- `COT_STRESS_CASCADE_RESOLUTION.txt`
- `COT_GOAL_PURSUIT_OPTIMIZATION.txt`
- `COT_ATTACHMENT_BEHAVIORAL_MAPPING.txt`
- `COT_PERFORMANCE_STATE_INTEGRATION.txt`
- `COT_MEMORY_FORMATION_CRITERIA.txt`
- `COT_DPF_SYNTHESIS_PROCESSING.txt`
- `COT_DECISION_SYNTHESIS.txt`
- `COT_COMMUNICATION_PROCESSING.txt`
- `COT_UPDATE_VERIFICATION.txt`

### Trait / lens modules (background psychology scaffolds)
- `P_HEXACO.txt`, `P_MMPI.txt`, `P_DARK_TRIAD.txt`, `P_ASQ.txt`, `P_COPE.txt`, `P_SHADOW_COT.txt`

---

## OTTC mapping (principles → files)

OTTC principle: Addressable ontology  
- `S_CANONICAL_TOKEN_DICTIONARY.txt`

OTTC principle: Propose → commit (single-writer reality)  
- `S_STATE_GOVERNANCE_OVERLAY.txt`
- `S_COGNITIVE_SCRATCHPAD.txt`
- `S_STATE_GOVERNANCE_AND_COMMIT.txt`

OTTC principle: Step limits + invariants + deterministic conflict resolution  
- `S_STATE_GOVERNANCE_OVERLAY.txt`
- `S_STATE_GOVERNANCE_AND_COMMIT.txt`

OTTC principle: Modifier layer (transient pressure without baseline erosion)  
- `S_TEMPORARY_MODIFIERS.txt`

OTTC principle: Epistemic output contract (player POV; no omniscience)  
- `COT_COMMUNICATION_PROCESSING.txt`
- `DOMINANT_PREDICTIVE_FRAME.txt` (subjective predictive stance)

OTTC principle: Predictive ledger (explicit hypotheses + contrast events)  
- `DOMINANT_PREDICTIVE_FRAME.txt`
- `COT_DPF_SYNTHESIS_PROCESSING.txt`

OTTC principle: Audit + verification (accountability)  
- `S_COGNITIVE_SCRATCHPAD.txt` (STATE_COMMIT_AUDIT)
- `COT_UPDATE_VERIFICATION.txt`

---

## Minimal “by hand” demo (no tools required)

To run a cycle in any chat UI:

1) Load the governance spine + the character modules.  
2) Provide a short narrative input (DM prompt).  
3) The system should produce:
   - scratchpad proposals and impulses (internal artifacts)
   - a single selected action
   - first-person player-style output
   - an audit record for every proposal
   - a verification trace result (PASS/WARN/FAIL)

If you don’t get audit + verification artifacts, you’re not running ChaOS as designed.

---

## License

Released under CC BY-SA 4.0. See `License.md`.

---

## OTTC (general pattern)

If you want the generalized architecture (not tied to character roleplay), see `OTTC_rendering.txt`.

