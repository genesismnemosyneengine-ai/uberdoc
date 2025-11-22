# uberdoc
# Multi-Agent Fiction Generation System - UBERDOC 3.0

**Version:** 3.0
**Date:** November 22, 2025
**Status:** Production-Ready (Phase 3.6 with Voice Differentiation)

---

## Table of Contents

1. [Executive Summary](#1-executive-summary)
2. [System Architecture](#2-system-architecture)
3. [Phase Evolution](#3-phase-evolution)
4. [Core Components](#4-core-components)
5. [Agent System](#5-agent-system)
6. [Memory & Psychology System (Phase 5)](#6-memory--psychology-system-phase-5)
7. [Prose-Level Voice Differentiation (Phase 3.6)](#7-prose-level-voice-differentiation-phase-36)
8. [State Management](#8-state-management)
9. [Prompt Engineering](#9-prompt-engineering)
10. [Configuration Reference](#10-configuration-reference)
11. [Entry Points & Usage](#11-entry-points--usage)
12. [Data Flow](#12-data-flow)
13. [Output Files](#13-output-files)
14. [Cost Estimates](#14-cost-estimates)
15. [Troubleshooting](#15-troubleshooting)

---

## 1. Executive Summary

### What This System Does

This is a **multi-agent AI fiction generation system** that produces psychologically realistic, narratively coherent stories through coordinated collaboration between specialized AI agents. The system goes beyond simple text generation to create stories with:

- **Long-term memory**: Characters remember events from many scenes ago
- **Psychological evolution**: Character personalities change based on trauma, bonding, and power dynamics
- **Relationship tracking**: Trust, tension, and intimacy evolve between character pairs
- **Narrative control**: Director-style orchestration ensures plot coherence and arc completion
- **Anti-stagnation**: Automatic detection and disruption of repetitive patterns
- **Distinct character voices**: Prose-level differentiation via example-driven style injection (NEW in 3.0)

### Key Achievement

The system has produced **literary-grade speculative fiction** comparable to published authors like Ted Chiang or Ken Liu. The output demonstrates:
- Thematic depth (epistemic horror, institutional corruption)
- Psychological realism (characters behave according to accumulated trauma)
- Narrative coherence (arcs open, develop, and close meaningfully)
- **Distinct character voices identifiable by prose style alone** (NEW in 3.0)

### Technology Stack

- **Language Model**: OpenAI gpt-5.1 (with reasoning_effort and verbosity parameters)
- **Embeddings**: OpenAI text-embedding-3-small (1536 dimensions)
- **Storage**: File-based (JSON, JSONL, NumPy)
- **Language**: Python 3.10+
- **API Client**: GPT5Client wrapper with role-specific configurations

---

## 2. System Architecture

### High-Level Architecture

```
┌─────────────────────────────────────────────────────────────────────┐
│                         AUTO-LAUNCHER                                │
│         (Generates story concepts, characters, arcs via LLM)        │
│         + Prose style specifications per character (Phase 3.6)      │
└────────────────────────────────┬────────────────────────────────────┘
                                 │
                                 ▼
┌─────────────────────────────────────────────────────────────────────┐
│                     PHASE 3.6 ORCHESTRATOR                          │
│                                                                      │
│  ┌─────────────────────────────────────────────────────────────┐   │
│  │                    PHASE 3 (DIRECTOR)                        │   │
│  │  • H₀-H₅ Prompt Stack    • 4-Stage Tactics                  │   │
│  │  • Arc Management        • Staleness Detection               │   │
│  │  • Completion Pressure   • Perturbation Injection            │   │
│  └─────────────────────────────────────────────────────────────┘   │
│                                                                      │
│  ┌─────────────────────────────────────────────────────────────┐   │
│  │                  PHASE 5 (ECOSYSTEM)                         │   │
│  │  • Vector Memory Store   • Personality Evolution             │   │
│  │  • Relationship Matrix   • Post-Scene Consolidation          │   │
│  │  • Embedding Cache       • LLM/Heuristic Analysis            │   │
│  └─────────────────────────────────────────────────────────────┘   │
│                                                                      │
│  ┌─────────────────────────────────────────────────────────────┐   │
│  │              PHASE 3.6 (VOICE DIFFERENTIATION)               │   │
│  │  • ProseStyle Model      • Example-Driven Directives         │   │
│  │  • Style Axes (8)        • Anti-Convergence Monitoring       │   │
│  │  • Prompt-Start Injection                                     │   │
│  └─────────────────────────────────────────────────────────────┘   │
└────────────────────────────────┬────────────────────────────────────┘
                                 │
                                 ▼
┌─────────────────────────────────────────────────────────────────────┐
│                      CHARACTER AGENTS                                │
│                                                                      │
│   ┌──────────┐    ┌──────────┐    ┌──────────┐    ┌──────────┐    │
│   │ Agent 1  │    │ Agent 2  │    │ Agent 3  │    │ Agent N  │    │
│   │(Protag)  │    │(Antag)   │    │ (Ally)   │    │  (...)   │    │
│   │ formal   │    │ stream   │    │ parent-  │    │  (...)   │    │
│   │ _self    │    │ _of_con  │    │ hetical  │    │          │    │
│   └──────────┘    └──────────┘    └──────────┘    └──────────┘    │
│                                                                      │
│   Each agent: Isolated conversation thread + Character sheet        │
│               + Phase 5 memory context + Personality state          │
│               + PROSE STYLE DIRECTIVE (injected before identity)    │
└─────────────────────────────────────────────────────────────────────┘
```

### Directory Structure

```
multi_agent_fiction/
├── agents/                    # AI agent implementations
│   ├── orchestrator_phase35.py   # Main orchestrator (Phase 3.5/3.6)
│   ├── orchestrator_phase3.py    # Phase 3 only
│   ├── character_agent.py        # Character representation
│   ├── context_builder.py        # Prompt construction with style injection
│   ├── scene_evaluator.py        # Post-scene quality assessment
│   ├── staleness_detector.py     # Pattern repetition + voice convergence detection
│   ├── idea_generator.py         # LLM-driven concept + prose style generation
│   └── methodology_selector.py   # Generation strategy selection
│
├── memory/                    # Memory & psychology systems
│   ├── phase5_engine.py          # Main Phase 5 interface
│   ├── vector_store.py           # Semantic memory storage
│   ├── personality_engine.py     # Character psychology evolution
│   ├── relationship_engine.py    # Interpersonal dynamics
│   ├── character_sheets.py       # Character definitions + ProseStyle model
│   └── scene_history.py          # Narrative sequence tracking
│
├── state/                     # Narrative state management
│   ├── arc_manager.py            # Story arc tracking
│   ├── progress_tracker.py       # Progress metrics
│   └── completion_checker.py     # Ending determination
│
├── prompts/                   # Prompt engineering
│   ├── h0_prime_directive.py     # Foundational constraints
│   ├── tactics.py                # 4-stage tactical guidance
│   └── perturbations.py          # Staleness disruption
│
├── config/                    # Configuration files
│   ├── story_config_phase3.json      # Story parameters
│   ├── character_config_phase3.json  # Character definitions
│   └── character_config_voice_test.json  # Voice differentiation test archetypes
│
├── utils/                     # Utilities
│   ├── api_client.py             # OpenAI API wrapper
│   └── logging.py                # Logging configuration
│
├── outputs/                   # Generated stories
│   ├── phase35_test_output.json  # Full structured output
│   └── phase35_narrative.txt     # Readable story
│
├── memory_data/               # Phase 5 storage (per-story isolation)
│   └── story_YYYYMMDD_HHMMSS/    # Timestamped story directories
│       ├── vector_store/
│       ├── personality_states.json
│       └── relationships.json
│
├── auto_launcher.py           # Main entry point (recommended)
├── main_phase35.py            # Direct Phase 3.5/3.6 entry
├── main_phase3.py             # Direct Phase 3 entry
└── story_manager.py           # Story management utility
```

---

## 3. Phase Evolution

### Phase 1: Basic Multi-Agent (Deprecated)
- Simple turn-taking between character agents
- No narrative control
- No memory persistence

### Phase 2: Orchestrator Introduction (Deprecated)
- Added orchestrator for scene management
- Basic arc tracking
- Still no long-term memory

### Phase 2.5: Turn-Based Dialogue (Deprecated)
- Improved dialogue flow
- Better character voice consistency
- No psychological modeling

### Phase 3: Director Mode (Active)
- **H₀-H₅ Prompt Stack**: Hierarchical prompt engineering
- **4-Stage Tactics**: Exploration → Escalation → Revelation → Convergence
- **Arc Management**: Urgency-based prioritization
- **Staleness Detection**: Pattern recognition across scenes
- **Perturbation Injection**: Automatic narrative disruption
- **Completion Pressure**: Budget-aware ending

### Phase 3.5: Hybrid Mode (Active)
All of Phase 3 **PLUS**:
- **Vector Memory Store**: Semantic search across all character memories
- **Personality Evolution**: 5-axis psychological tracking
- **Relationship Dynamics**: Trust/tension/intimacy between character pairs
- **Post-Scene Consolidation**: Automatic state updates after each scene

### Phase 3.6: Voice Differentiation (Active - NEW)
All of Phase 3.5 **PLUS**:
- **ProseStyle Model**: 8-axis prose specification per character
- **Example-Driven Directives**: Concrete first-person POV examples, not abstract descriptions
- **Prompt-Start Injection**: Style directive placed BEFORE character identity
- **Anti-Convergence Monitoring**: Detection of voice collapse into house style
- **Auto-Launcher Integration**: LLM generates diverse prose_style specs for each character

**The Breakthrough**: Abstract style description → Concrete first-person POV examples, injected before character identity.

### Phase 5: Ecosystem (Integrated into Phase 3.5/3.6)
The Phase 5 systems are now fully integrated:
- Memory retrieval before character generation
- Personality context injection
- Relationship awareness
- Consolidated updates after scene completion

---

## 4. Core Components

### 4.1 OrchestratorPhase35

**File:** `agents/orchestrator_phase35.py`

The central controller that manages the entire story generation process.

**Responsibilities:**
- Scene setup (participants, goals, tactics)
- Speaker selection within scenes
- Arc management and closure
- Phase 5 memory/personality integration
- Completion checking

**Key Methods:**
```python
decide_scene_setup()      # Choose who participates and scene goal
decide_next_speaker()     # Select next character to speak
is_scene_complete()       # Check if scene achieved its goal
check_completion()        # Determine if story should end
consolidate_scene()       # Post-scene Phase 5 updates
```

### 4.2 CharacterAgent

**File:** `agents/character_agent.py`

Represents individual characters as isolated LLM conversation threads.

**Features:**
- Maintains conversation history
- Receives character sheet context
- Receives Phase 5 memory/personality context
- **Receives prose style directive (Phase 3.6)**
- Generates dialogue in character voice

**Key Methods:**
```python
generate_turn()           # Generate single dialogue turn
get_conversation_history()  # Retrieve full thread
reset_conversation()      # Clear history
```

### 4.3 ContextBuilder

**File:** `agents/context_builder.py`

Constructs the full prompt for character agents.

**Phase 3.6 Enhancement:**
```python
# START with prose style directive (BEFORE identity) for maximum override effect
prompt = ""
if identity.get('prose_style_directive'):
    prompt = f"""{identity['prose_style_directive']}

---

"""
prompt += f"""You are {identity['name']}."""
```

**Key Insight**: Positioning the style directive BEFORE identity establishment ensures the style constraints are internalized before the character "persona" is activated.

### 4.4 SceneEvaluator

**File:** `agents/scene_evaluator.py`

Post-scene analysis using LLM to assess quality and arc progress.

**Evaluates:**
- Arc closure (was this arc resolved?)
- Character goal progress
- Scene quality (prose, tension, authenticity, advancement)
- Secrets revealed

**Key Methods:**
```python
evaluate_scene_outcomes()  # Analyze arc closure
evaluate_scene_quality()   # Rate 1-5 on multiple dimensions
```

### 4.5 StalenessDetector

**File:** `agents/staleness_detector.py`

Identifies repetitive patterns to prevent narrative stagnation.

**Analyzes:**
- Keyword repetition
- Location repetition
- Interaction patterns (character pairings)
- Semantic similarity between scenes
- Narrative beat repetition
- **Prose convergence (Phase 3.6)**: Detection of voice collapse

**Phase 3.6 Addition:**
```python
class ProseConvergenceMetrics:
    """Tracks whether character voices are converging toward house style."""
    thought_format_variance: float  # Should stay high
    sentence_complexity_variance: float
    sensory_focus_variance: float
```

**Key Methods:**
```python
analyze_staleness()       # Comprehensive staleness analysis
should_perturb()          # Determine if disruption needed
detect_prose_convergence()  # NEW: Check if voices are collapsing
```

---

## 5. Agent System

### 5.1 IdeaGenerator

**File:** `agents/idea_generator.py`

Uses LLM to generate complete story concepts from minimal input.

**Generates:**
- Story concept (title, genre, tone, premise, logline)
- Character roster (3-6 characters with full definitions)
- **Prose style specifications per character (Phase 3.6)**
- Narrative arcs (5+ arcs with scene allocations)

**Phase 3.6 Enhancement:**

The idea generator now requests diverse prose_style specs:

```
For EACH character, specify a distinct prose_style with:
- internal_thoughts_format: MUST vary between characters
  Options: parenthetical, stream_of_consciousness, second_person_imperative, formal_self_address, none
- sentence_complexity: MUST vary between characters
  Options: simple_declarative, compound, complex_subordinate, fragments, mixed
- sensory_focus: MUST vary between characters
  Options: visual, kinesthetic, auditory, olfactory, abstract
- paragraph_rhythm: staccato, flowing, jagged, measured, breathless
- metaphor_density: sparse, moderate, heavy
- vocabulary_register: colloquial, working_class, educated, academic, technical, poetic
- unique_stylistic_markers: List of 3-4 specific prose tics unique to this character
- never_does: List of things this character's prose NEVER does (author reference only)

PROSE STYLE DIVERSITY RULES:
- No two characters may share the same internal_thoughts_format
- No two characters may share the same sentence_complexity
- At least 3 different sensory_focus values across the cast
```

**Parameters:**
- `genre`: Optional genre preference
- `theme`: Optional thematic focus
- `novelty`: 0.0-1.0 (classic tropes to experimental)
- `scene_count`: Target number of scenes

### 5.2 MethodologySelector

**File:** `agents/methodology_selector.py`

Strategically selects generation approach and parameters.

**Selects:**
- Mode: fiction vs problem-solving
- Reasoning effort levels (orchestrator, agents, evaluator)
- Pacing strategy (scene-by-scene breakdown)
- Quality criteria by genre

### 5.3 Agent Interaction Flow

```
1. IdeaGenerator creates concept, characters (with prose_style), arcs
2. MethodologySelector optimizes pacing strategy
3. OrchestratorPhase35 runs scene loop:
   a. decide_scene_setup() → participants, goal, tactic
   b. For each turn:
      - decide_next_speaker() → which character
      - CharacterAgent.generate_turn() → dialogue
        (with prose_style_directive injected FIRST)
      - Phase5Engine.store_turn() → save to memory
   c. is_scene_complete() → check goal achievement
   d. SceneEvaluator.evaluate_scene_outcomes() → arc closure
   e. Phase5Engine.consolidate_scene() → update psychology
4. check_completion() → should story end?
5. Repeat until completion criteria met
```

---

## 6. Memory & Psychology System (Phase 5)

### 6.1 Phase5Engine

**File:** `memory/phase5_engine.py`

Main interface for all Phase 5 functionality.

**Capabilities:**
- Store dialogue turns with embeddings
- Retrieve relevant memories via semantic search
- Track personality evolution
- Manage relationship dynamics
- Post-scene consolidation
- **Store prose_style_fingerprint with each turn (Phase 3.6)**

**Key Methods:**
```python
store_turn(turn_data)              # Save dialogue to memory (includes prose fingerprint)
get_relevant_memories(character_id, context, directive, top_k)
get_character_state(character_id)  # Get personality
get_relationship(char1, char2)     # Get relationship
consolidate_scene(scene_content, participants)  # Post-scene updates
```

### 6.2 VectorMemoryStore

**File:** `memory/vector_store.py`

Semantic memory storage and retrieval.

**Storage:**
- `memories.jsonl`: Memory metadata (character, timestamp, content, etc.)
- `embeddings.npy`: NumPy array of embedding vectors

**Retrieval:**
```python
search(query_embedding, character_id=None, top_k=5, min_score=0.5)
```
Uses cosine similarity to find relevant memories.

### 6.3 PersonalityEvolutionEngine

**File:** `memory/personality_engine.py`

Tracks character psychology across 5 axes:

| Axis | Range | Description |
|------|-------|-------------|
| **Trauma** | 0-10 | Accumulated psychological wounds |
| **Bonding** | 0-10 | Connection to others |
| **Power** | 0-10 | Sense of control/agency |
| **Trust in Others** | 0-10 | Openness vs paranoia |
| **Emotional Volatility** | 0-10 | Stability vs breakdown |

**Update Triggers:**
- Betrayal → trauma↑, bonding↓, trust↓
- Violence witnessed → trauma↑, power↓
- Secret learned → varies by content
- Connection formed → bonding↑, trust↑

**Modes:**
- **LLM Analysis**: GPT analyzes scene for psychological impact
- **Heuristic**: Keyword-based pattern matching (faster/cheaper)

### 6.4 RelationshipMatrixEngine

**File:** `memory/relationship_engine.py`

Tracks bidirectional relationships between character pairs.

**Metrics:**
| Metric | Range | Description |
|--------|-------|-------------|
| **Trust** | 0-1 | Reliability/dependability |
| **Tension** | 0-1 | Conflict/opposition |
| **Intimacy** | 0-1 | Emotional closeness |

**Additional Tracking:**
- `shared_secrets`: List of secrets known by both
- `significant_moments`: Key relationship events
- `interaction_count`: Number of interactions

### 6.5 Memory Isolation

Each story gets isolated memory storage:

```
memory_data/
├── story_20251121_151700/    # Story 1 (isolated)
│   ├── vector_store/
│   ├── personality_states.json
│   └── relationships.json
└── story_20251121_163400/    # Story 2 (isolated)
    └── ...
```

**Benefits:**
- No memory contamination between stories
- Easy comparison of different runs
- Sequel support via `resume_from` parameter

---

## 7. Prose-Level Voice Differentiation (Phase 3.6)

### 7.1 The Problem

Multi-agent fiction systems suffer from "one author writing multiple characters" syndrome. Despite different backstories and motivations, all characters sound the same:

- Same parenthetical thought patterns: `(Something wrong here.)`
- Same sentence rhythms and lengths
- Same sensory focus (usually visual)
- Same metaphor density
- Same vocabulary register

**Result**: Readers cannot identify who is speaking without dialogue tags.

### 7.2 The Solution: ProseStyle Model

**File:** `memory/character_sheets.py`

Each character receives a `ProseStyle` specification with 8 axes:

```python
class ProseStyle(BaseModel):
    internal_thoughts_format: str = Field(
        default="parenthetical",
        description="How internal thoughts are expressed"
    )
    # Options: parenthetical | stream_of_consciousness | second_person_imperative | formal_self_address | none

    sentence_complexity: str = Field(
        default="mixed",
        description="Sentence structure"
    )
    # Options: simple_declarative | compound | complex_subordinate | fragments | mixed

    paragraph_rhythm: str = Field(
        default="measured",
        description="Prose rhythm"
    )
    # Options: staccato | flowing | jagged | measured | breathless

    sensory_focus: str = Field(
        default="visual",
        description="Primary sensory mode"
    )
    # Options: visual | kinesthetic | auditory | olfactory | abstract

    metaphor_density: str = Field(
        default="moderate",
        description="Use of figurative language"
    )
    # Options: sparse | moderate | heavy

    vocabulary_register: str = Field(
        default="educated",
        description="Word choice level"
    )
    # Options: colloquial | working_class | educated | academic | technical | poetic

    unique_stylistic_markers: List[str] = Field(
        default_factory=list,
        description="Specific tics, repeated constructions unique to this character"
    )

    never_does: List[str] = Field(
        default_factory=list,
        description="Counter-examples (author reference only, not injected)"
    )
```

### 7.3 The Breakthrough: Example-Driven Directives

Abstract style descriptions fail because:
- "Measured prose rhythm" is interpretable many ways
- Negative rules ("NEVER uses parenthetical thoughts") require remembering what NOT to do
- Style specs buried in character backstory get deprioritized

**The solution: Concrete first-person POV examples.**

```python
def to_style_directive(self, character_name: str) -> str:
    """Convert prose style to an override directive with concrete examples."""
    directive = f"""WRITE {character_name.upper()} EXACTLY LIKE THIS:

{self._get_thought_example(character_name)}

{self._get_sentence_example()}

{self._get_sensory_example()}
"""
    if self.unique_stylistic_markers:
        directive += f"\n{character_name.upper()}'S SIGNATURE TECHNIQUES (use these):\n"
        for marker in self.unique_stylistic_markers:
            directive += f"• {marker}\n"

    directive += f"""
Match the examples above. This is how {character_name} sounds."""

    return directive
```

### 7.4 Example Generation

Each helper method returns concrete examples in first-person POV:

**Thought Examples:**
```python
def _get_thought_example(self, character_name: str) -> str:
    examples = {
        "parenthetical": """THOUGHTS — Write inner thoughts in parentheses:
EXAMPLE: The door stood open. (Something wrong here.) I stepped inside carefully.""",

        "stream_of_consciousness": """THOUGHTS — Weave thoughts directly into the prose, no parentheses, no markers, thoughts and observations blur together:
EXAMPLE: The door stood open and something was wrong here, I could feel it in the way the air moved, the way dust hung still where it should have scattered, and I stepped inside with my hand already reaching for the wall.""",

        "second_person_imperative": """THOUGHTS — Inner voice gives commands to self:
EXAMPLE: The door stood open. Stay alert. Check the corners first. I stepped inside carefully.""",

        "formal_self_address": f"""THOUGHTS — Refer to self by name or title, almost dissociatively:
EXAMPLE: The door stood open. {character_name} noted the irregularity; {character_name} would proceed with appropriate caution. I stepped inside.""",

        "none": """THOUGHTS — Show only external actions, dialogue, and observable behavior. No inner thoughts at all:
EXAMPLE: The door stood open. I stepped inside carefully, one hand on the doorframe."""
    }
    return examples.get(self.internal_thoughts_format, examples["parenthetical"])
```

**Sentence Examples:**
```python
def _get_sentence_example(self) -> str:
    examples = {
        "simple_declarative": """SENTENCES — Short and direct. One thought per sentence:
EXAMPLE: I found the room dark. I saw a chair overturned. Glass on the floor. I waited.""",

        "compound": """SENTENCES — Chain thoughts together with 'and', 'but', 'so':
EXAMPLE: I found the room dark and saw a chair overturned near the window, but the glass on the floor caught what little light came through, so I waited and listened.""",

        "complex_subordinate": """SENTENCES — Nest clauses inside clauses, layer qualifications:
EXAMPLE: The room, which had been bright when I left that morning, was dark now, the chair—the one I had always kept by the window—overturned in a way that suggested haste, near where glass lay scattered in a pattern that spoke of force from within rather than without.""",

        "fragments": """SENTENCES — Use fragments. Incomplete thoughts. Let gaps do work:
EXAMPLE: Dark room. Chair down. Glass everywhere. I wait. I listen. Nothing yet.""",

        "mixed": """SENTENCES — Vary length. Short for impact, long when building:
EXAMPLE: I found the room dark. A chair lay overturned near the window, its legs pointing outward like accusation, and glass covered the floor in a pattern I would remember later, when the questions started. I waited."""
    }
    return examples.get(self.sentence_complexity, examples["mixed"])
```

**Sensory Examples:**
```python
def _get_sensory_example(self) -> str:
    examples = {
        "visual": """SENSES — Focus on what is seen. Light, shadow, color, movement, faces:
EXAMPLE: I watched the lamplight catch the edge of a jaw, the line of a throat. I saw hands stay flat on the table, fingers spread wide, knuckles pale.""",

        "kinesthetic": """SENSES — Focus on body sensations. Tension, weight, temperature, pressure:
EXAMPLE: My shoulders pulled tight. I felt the chair press cold through my clothes. My fingers wanted to curl into fists but I kept them flat, kept them still.""",

        "auditory": """SENSES — Focus on sounds. Voice quality, silence, ambient noise:
EXAMPLE: I heard a voice come low and rough, scraping against the quiet. Outside, wind tested the shutters. I listened to the lamp hiss its small complaint.""",

        "olfactory": """SENSES — Focus on smell. Let scent trigger memory and mood:
EXAMPLE: I smelled old tobacco and lamp oil, underneath it something sharper—fear-sweat, maybe, or the ghost of whiskey from a broken bottle.""",

        "abstract": """SENSES — Focus on patterns, concepts, logic. Process through ideas:
EXAMPLE: I saw the arrangement make sense now. Each piece connecting: the letter, the timing, the convenient absence. I recognized a design, not an accident."""
    }
    return examples.get(self.sensory_focus, examples["visual"])
```

### 7.5 Prompt Injection Position

**Critical architectural decision**: The style directive is injected BEFORE character identity.

**File:** `agents/context_builder.py`

```python
# START with prose style directive (BEFORE identity) for maximum override effect
prompt = ""
if identity.get('prose_style_directive'):
    prompt = f"""{identity['prose_style_directive']}

---

"""
prompt += f"""You are {identity['name']}."""
```

**Why this works**: The LLM sees the concrete examples before it gets "into character," so the style constraints are established first. The character identity then operates within those constraints.

### 7.6 Architecture: Two-Level Style Control

```
┌─────────────────────────────────────────────────┐
│  H₀ Prime Directive (SHARED)                    │
│  "Western frontier drama, tense, morally gray"  │
└─────────────────────────────────────────────────┘
                      ↓
┌─────────────────────────────────────────────────┐
│  Per-Character Prose Style Directive            │
│  ┌─────────────────┬─────────────┬───────────┐ │
│  │ Sheriff:        │ Outlaw:     │ Widow:    │ │
│  │ formal_self     │ stream_of   │ parenthe- │ │
│  │ _address,       │ conscious,  │ tical,    │ │
│  │ complex_        │ fragments,  │ mixed,    │ │
│  │ subordinate,    │ kinesthetic │ flowing,  │ │
│  │ abstract        │             │ visual,   │ │
│  │                 │             │ poetic    │ │
│  └─────────────────┴─────────────┴───────────┘ │
└─────────────────────────────────────────────────┘
                      ↓
┌─────────────────────────────────────────────────┐
│  Character Identity (name, backstory, secrets)  │
└─────────────────────────────────────────────────┘
```

**Key insight**: **Prose style is orthogonal to genre.**

A "kinesthetic, fragmented" voice can exist in gothic horror OR frontier western OR literary realism. The style directive controls *how* the character narrates; the Prime Directive controls *what kind of story* they're narrating.

This is the correct architecture because:
1. **Genre coherence** - All characters inhabit the same story world with the same tonal expectations
2. **Voice differentiation** - Each character *sounds* different while *belonging* to the same narrative

### 7.7 Sample Generated Prose Styles

Example from auto_launcher generating a Western story:

**Sheriff (Miriam Kline):**
```json
{
  "internal_thoughts_format": "formal_self_address",
  "sentence_complexity": "complex_subordinate",
  "paragraph_rhythm": "measured",
  "sensory_focus": "abstract",
  "metaphor_density": "moderate",
  "vocabulary_register": "educated",
  "unique_stylistic_markers": [
    "Frequently frames thoughts as if addressing herself by title",
    "Uses balanced, triadic structures",
    "Introduces logical connectors explicitly"
  ]
}
```

**Outlaw (Cassian "Cass" Rye):**
```json
{
  "internal_thoughts_format": "stream_of_consciousness",
  "sentence_complexity": "fragments",
  "paragraph_rhythm": "jagged",
  "sensory_focus": "kinesthetic",
  "metaphor_density": "sparse",
  "vocabulary_register": "working_class",
  "unique_stylistic_markers": [
    "Frequent run-on coordination with 'and' and 'but'",
    "Short, blunt fragments dropped to undercut",
    "Physical sensations stand in for named feelings"
  ]
}
```

**Widow (Alma Villarreal):**
```json
{
  "internal_thoughts_format": "parenthetical",
  "sentence_complexity": "mixed",
  "paragraph_rhythm": "flowing",
  "sensory_focus": "visual",
  "metaphor_density": "heavy",
  "vocabulary_register": "poetic",
  "unique_stylistic_markers": [
    "Frequent parenthetical asides revealing private thoughts",
    "Rich visual similes drawn from domestic work",
    "Repetition of key phrases as incantation"
  ]
}
```

### 7.8 Anti-Convergence Monitoring

**File:** `agents/staleness_detector.py`

Over time, character voices may "collapse" toward a house style. The staleness detector now monitors for this:

```python
class ProseConvergenceMetrics:
    """Tracks whether character voices are converging toward house style."""
    thought_format_variance: float  # Should stay high
    sentence_complexity_variance: float
    sensory_focus_variance: float

def detect_prose_convergence(self, recent_outputs: Dict[str, List[str]]) -> float:
    """
    Analyze recent outputs for voice convergence.
    Returns 0.0 (distinct voices) to 1.0 (collapsed to house style).
    """
    # Implementation analyzes structural markers across character outputs
```

### 7.9 Testing Voice Differentiation

**Flag:** `--voice-test` on `main_phase35.py`

```bash
python main_phase35.py --voice-test
```

Uses `config/character_config_voice_test.json` with extreme style archetypes:

1. **The Minimalist**: `simple_declarative`, `fragments`, `kinesthetic`, `sparse`
2. **The Baroque**: `complex_subordinate`, `flowing`, `visual`, `heavy`
3. **The Fragmentary**: `fragments`, `jagged`, `auditory`, `sparse`
4. **The Procedural**: `formal_self_address`, `compound`, `abstract`, `moderate`

### 7.10 Cross-Story Voice Persistence (Experimental)

**Question**: Do character prose styles persist across genre boundaries?

**Test Design**:
1. Define fixed style archetypes (independent of story content)
2. Run auto_launcher with Genre A (frontier western)
3. Run auto_launcher with Genre B (gothic horror)
4. Apply same style archetypes to generated characters
5. Compare outputs: Can you identify archetype regardless of genre?

**Prediction**: ~80% persistence. Structural markers (fragments vs subordinate clauses, parenthetical vs stream-of-consciousness) should hold, while genre-specific vocabulary naturally varies.

---

## 8. State Management

### 8.1 ArcManager

**File:** `state/arc_manager.py`

Manages story arcs with urgency-based prioritization.

**Arc Properties:**
```python
@dataclass
class StoryArc:
    id: str
    description: str
    importance: float          # 0.0-1.0
    scenes_remaining: int      # Budget for this arc
    characters: List[str]      # Involved characters
    resolution: str            # What closure looks like
    status: str                # "open" or "closed"
    satisfaction: float        # 0.0-5.0 (when closed)
```

**Urgency Calculation:**
```python
urgency = importance / max(scenes_remaining, 1)
```
Higher urgency = arc needs attention soon.

### 8.2 ProgressTracker

**File:** `state/progress_tracker.py`

Tracks overall story progress.

**Metrics:**
- Scene index and word count
- Character goal progress
- Open/closed arc counts
- Tension curve
- Budget remaining (scenes/words)

### 8.3 CompletionChecker

**File:** `state/completion_checker.py`

Determines when story should end.

**Completion Criteria:**
1. Word budget exhausted (>90%)
2. Scene budget exhausted
3. All arcs closed
4. All character goals resolved
5. Combined criteria (configurable)

**Completion Pressure:**
```python
pressure = max(word_usage, scene_usage)
# 0.0 = beginning, 1.0 = must end now
```

---

## 9. Prompt Engineering

### 9.1 H₀-H₅ Prompt Stack

Hierarchical prompt layers, each adding constraints:

| Layer | Name | Purpose | Mutability |
|-------|------|---------|------------|
| **H₀** | Prime Directive | Genre, tone, meta-constraints | Immutable |
| **H₁** | Story Bible | Arcs, character sheets, current state | Updated per scene |
| **H₂** | Live Scratchpad | Recent events, current goal | Updated per turn |
| **H₃** | Arc Targeting | Which arc to advance, urgency | Updated per scene |
| **H₄** | Tactical Guidance | Current tactic (explore/escalate/etc.) | Updated per scene |
| **H₅** | Novelty Pressure | Perturbation if stale | Conditional |
| **H₆** | **Prose Style Directive** (NEW) | Example-driven voice constraints | Per-character |

**Note**: H₆ (Prose Style Directive) is injected BEFORE character identity for maximum effect.

### 9.2 Tactics System

**File:** `prompts/tactics.py`

4-stage tactical progression:

**Stage 1: Exploration (0-40% complete)**
- `explore`: Investigate setting/situation
- `complicate`: Introduce obstacles
- `deepen_character`: Reveal psychology
- `build_relationship`: Develop connections
- `introduce_mystery`: Plant questions

**Stage 2: Escalation (40-60% complete)**
- `increase_pressure`: Tighten constraints
- `worsen_situation`: Stakes rise
- `raise_personal_stakes`: Character investment
- `force_difficult_choice`: Dilemmas
- `escalate_conflict`: Confrontation

**Stage 3: Revelation (60-80% complete)**
- `expose_secret`: Truth emerges
- `connect_clues`: Pieces fit together
- `force_confession`: Characters admit truth
- `discover_evidence`: Proof found
- `witness_truth`: Direct observation

**Stage 4: Convergence (80-100% complete)**
- `nudge_climax`: Push toward ending
- `force_resolution`: Close open threads
- `mirror_scene`: Callback to beginning
- `time_jump`: Skip to aftermath
- `final_confrontation`: Decisive moment

### 9.3 Perturbation System

**File:** `prompts/perturbations.py`

Automatic narrative disruption when staleness detected.

**Perturbations by Severity:**

| Severity | Perturbations |
|----------|---------------|
| 0.3 (Light) | unexpected_visitor, environmental_change, sensory_disruption |
| 0.5 (Medium) | urgent_message, object_discovered, minor_crisis, schedule_pressure |
| 0.7 (Strong) | forced_separation, partial_revelation, external_threat |
| 0.9 (Severe) | forced_choice, reversal |

**Selection Logic:**
- Low staleness (0.3-0.5): Light perturbation
- Medium staleness (0.5-0.7): Medium perturbation
- High staleness (0.7-0.85): Strong perturbation
- Severe staleness (>0.85): Severe perturbation

---

## 10. Configuration Reference

### 10.1 Story Configuration

**File:** `config/story_config_phase3.json`

```json
{
  "title": "Story Title",
  "genre": "gothic horror",
  "tone": "dark, atmospheric, suspenseful",
  "meta_constraint": "Additional narrative constraints",
  "completion_criteria": "All arcs closed, character goals resolved",
  "constraints": "No graphic violence. Psychological horror only.",
  "planned_length": {
    "scenes": 15,
    "words": 8000
  },
  "logline": "One-sentence story summary",
  "initial_arcs": [
    {
      "description": "Arc description",
      "importance": 0.9,
      "scenes_remaining": 10,
      "characters": ["protagonist", "antagonist"],
      "resolution": "What closure looks like"
    }
  ],
  "character_goals": {
    "protagonist": "What the protagonist wants to achieve"
  }
}
```

### 10.2 Character Configuration (Phase 3.6 Enhanced)

**File:** `config/character_config_phase3.json`

```json
{
  "characters": [
    {
      "id": "protagonist",
      "name": "Character Name",
      "core_traits": ["curious", "determined", "analytical"],
      "voice": "First person, introspective, analytical",
      "backstory": "Character history and context",
      "motivations": ["goal 1", "goal 2"],
      "secrets": ["secret 1", "secret 2"],
      "initial_knowledge": {
        "knows_about": ["fact 1", "fact 2"],
        "believes": ["belief 1", "belief 2"],
        "has_observed": []
      },
      "initial_emotional_state": "anxious but determined",
      "prose_style": {
        "internal_thoughts_format": "parenthetical",
        "sentence_complexity": "mixed",
        "paragraph_rhythm": "measured",
        "sensory_focus": "visual",
        "metaphor_density": "moderate",
        "vocabulary_register": "educated",
        "unique_stylistic_markers": [
          "Uses rhetorical questions before revelations",
          "Returns to specific imagery when stressed"
        ],
        "never_does": [
          "Never uses profanity",
          "Never writes sentence fragments"
        ]
      }
    }
  ]
}
```

### 10.3 Methodology Configuration

Auto-generated by `MethodologySelector`:

```json
{
  "mode": "fiction",
  "scene_count": 14,
  "reasoning_efforts": {
    "orchestrator": "high",
    "agents": "medium",
    "evaluator": "medium"
  },
  "use_phase35": true,
  "phase5_enabled": true,
  "phase5_use_llm": false,
  "pacing_strategy": {
    "stage_breakdown": [...],
    "arc_closure_schedule": {...}
  }
}
```

---

## 11. Entry Points & Usage

### 11.1 AUTO_LAUNCHER (Recommended)

**File:** `auto_launcher.py`

Fully automated story generation with LLM-driven ideation.

```bash
python auto_launcher.py
```

**Modes:**
1. **Interactive**: You choose preferences, LLM generates ideas
2. **Fully Automatic**: LLM decides everything

**Options:**
- Genre preference (or let LLM choose)
- Novelty level (0.0-1.0)
- Scene count (10-25)
- Phase selection (Phase 3 or Phase 3.5/3.6)
- Phase 5 options (disabled/heuristics/LLM)

**Phase 3.6 Enhancement:**
The auto_launcher now generates prose_style specifications for each character and displays them during interactive mode:

```
Character: Sheriff Miriam Kline
  Prose Style: formal_self_address | complex_subordinate | abstract
```

### 11.2 Direct Phase 3.5/3.6

**File:** `main_phase35.py`

Run Phase 3.5/3.6 directly with existing configs.

```bash
# Standard run
python main_phase35.py

# Voice differentiation test
python main_phase35.py --voice-test
```

**Programmatic Usage:**
```python
from main_phase35 import main

# New story (isolated memory)
story_path = main()

# Sequel/continuation
main(resume_from="memory_data/story_20251121_151700")
```

### 11.3 Direct Phase 3

**File:** `main_phase3.py`

Run Phase 3 without Phase 5/3.6 features.

```bash
python main_phase3.py
```

### 11.4 Story Manager

**File:** `story_manager.py`

Utility for managing stored stories.

```bash
# List all stories
python story_manager.py list

# Inspect story details
python story_manager.py inspect memory_data/story_20251121_151700

# Resume instructions
python story_manager.py resume memory_data/story_20251121_151700
```

---

## 12. Data Flow

### 12.1 Scene Generation Flow (Phase 3.6)

```
┌─────────────────────────────────────────────────────────────────┐
│ SCENE SETUP                                                      │
│                                                                  │
│ 1. Orchestrator.decide_scene_setup()                            │
│    - Select participants based on arc urgency                    │
│    - Choose scene goal                                           │
│    - Select tactic (exploration/escalation/revelation/convergence)│
│    - Check staleness → inject perturbation if needed            │
└────────────────────────────────┬────────────────────────────────┘
                                 │
                                 ▼
┌─────────────────────────────────────────────────────────────────┐
│ TURN-BASED DIALOGUE                                              │
│                                                                  │
│ For each turn:                                                   │
│ 2. Orchestrator.decide_next_speaker()                           │
│    - Consider arc needs, fairness, last speaker                 │
│                                                                  │
│ 3. Phase5Engine.get_relevant_memories(character_id, context)    │
│    Phase5Engine.get_character_state(character_id)               │
│    Phase5Engine.get_relationship(char1, char2)                  │
│                                                                  │
│ 4. ContextBuilder.build_prompt()                                │
│    - FIRST: Inject prose_style_directive (Phase 3.6)            │
│    - THEN: Character identity, backstory, knowledge             │
│    - Phase 5 context (memories, personality, relationships)     │
│    - H₀-H₅ prompt stack                                         │
│                                                                  │
│ 5. CharacterAgent.generate_turn()                               │
│    - Receives: Full prompt with style directive at start        │
│    - Outputs: In-character dialogue/action with distinct voice  │
│                                                                  │
│ 6. Phase5Engine.store_turn(turn_data)                           │
│    - Embed text, calculate importance                           │
│    - Store in vector memory                                     │
│    - Record prose_style_fingerprint (Phase 3.6)                 │
└────────────────────────────────┬────────────────────────────────┘
                                 │
                                 ▼
┌─────────────────────────────────────────────────────────────────┐
│ SCENE COMPLETION                                                 │
│                                                                  │
│ 7. Orchestrator.is_scene_complete()                             │
│    - Check if scene goal achieved                               │
│    - Check turn limit                                           │
│                                                                  │
│ 8. SceneEvaluator.evaluate_scene_outcomes()                     │
│    - Determine arc closure                                      │
│    - Assess character goal progress                             │
│                                                                  │
│ 9. SceneEvaluator.evaluate_scene_quality()                      │
│    - Rate prose, tension, authenticity, advancement             │
│                                                                  │
│ 10. StalenessDetector.detect_prose_convergence() (Phase 3.6)    │
│     - Check if character voices are collapsing                  │
│                                                                  │
│ 11. Phase5Engine.consolidate_scene()                            │
│     - Store scene summary memory                                │
│     - Update personality states (trauma, bonding, etc.)         │
│     - Update relationship dynamics (trust, tension, intimacy)   │
└────────────────────────────────┬────────────────────────────────┘
                                 │
                                 ▼
┌─────────────────────────────────────────────────────────────────┐
│ COMPLETION CHECK                                                 │
│                                                                  │
│ 12. Orchestrator.check_completion()                             │
│     - Word/scene budget exhausted?                              │
│     - All arcs closed?                                          │
│     - All character goals resolved?                             │
│                                                                  │
│ If not complete → return to SCENE SETUP                         │
│ If complete → save outputs and exit                             │
└─────────────────────────────────────────────────────────────────┘
```

### 12.2 Memory Retrieval Flow

```
Character needs to generate dialogue
            │
            ▼
┌─────────────────────────────────────┐
│ Build query from:                    │
│ - Current scene context              │
│ - Scene goal                         │
│ - Character's directive              │
└───────────────┬─────────────────────┘
                │
                ▼
┌─────────────────────────────────────┐
│ Embed query via EmbeddingWorker     │
│ (with caching)                       │
└───────────────┬─────────────────────┘
                │
                ▼
┌─────────────────────────────────────┐
│ VectorMemoryStore.search()          │
│ - Cosine similarity                  │
│ - Filter by character_id             │
│ - Top-K results                      │
│ - Min score threshold (0.5)          │
└───────────────┬─────────────────────┘
                │
                ▼
┌─────────────────────────────────────┐
│ Format memories for prompt:          │
│ "You remember:                       │
│  - [Scene 3] The confession...       │
│  - [Scene 7] The discovery..."       │
└─────────────────────────────────────┘
```

---

## 13. Output Files

### 13.1 Story Output

**Primary Output:** `outputs/phase35_test_output.json`

```json
{
  "story_config": {...},
  "scenes": [
    {
      "scene_index": 0,
      "participants": ["protagonist", "antagonist"],
      "goal": "Discover the first clue",
      "tactic": "exploration",
      "turns": [
        {
          "speaker": "protagonist",
          "content": "I stepped into the archive...",
          "timestamp": 0.0
        }
      ],
      "quality_scores": {
        "prose": 4.0,
        "tension": 4.5,
        "authenticity": 4.0,
        "advancement": 4.5
      }
    }
  ],
  "final_summary": {...}
}
```

**Readable Narrative:** `outputs/phase35_narrative.txt`

Plain text version of the story for reading.

### 13.2 Phase 5 Data

**Memory Storage:** `memory_data/story_YYYYMMDD_HHMMSS/`

**Vector Store:**
- `vector_store/memories.jsonl`: Memory metadata
- `vector_store/embeddings.npy`: Embedding vectors

**Psychology:**
- `personality_states.json`: Character personality tracking
- `relationships.json`: Relationship matrices

**Cache:**
- `embedding_cache/cache.jsonl`: Embedding cache for efficiency

---

## 14. Cost Estimates

### Token Usage (Per Story)

| Mode | 15 Scenes | 25 Scenes | 100 Scenes |
|------|-----------|-----------|------------|
| Phase 3 only | ~150K-300K tokens | ~250K-500K tokens | ~1M-2M tokens |
| Phase 3.5 (heuristics) | ~165K-330K tokens | ~275K-550K tokens | ~1.1M-2.2M tokens |
| Phase 3.6 (voice diff) | ~170K-340K tokens | ~285K-570K tokens | ~1.15M-2.3M tokens |
| Phase 3.5/3.6 (LLM analysis) | ~220K-450K tokens | ~370K-750K tokens | ~1.5M-3M tokens |

**Note**: Phase 3.6 adds minimal token overhead (~3-5%) because the prose style directive is a fixed-size injection per turn.

### AUTO_LAUNCHER Overhead

- Concept generation: ~5K-10K tokens
- Character generation (with prose_style): ~7K-12K tokens (+2K for style specs)
- Arc generation: ~5K-10K tokens
- Methodology selection: ~2K-5K tokens
- **Total overhead**: ~19K-37K tokens per run

### Cost Optimization Tips

1. Use heuristics instead of LLM analysis for Phase 5
2. Reduce scene count for testing
3. Lower `reasoning_effort` parameter (low vs high)
4. Use Phase 3 for quick experiments

---

## 15. Troubleshooting

### Common Issues

**"Config file not found"**
```bash
cd /mnt/c/newproject/multi_agent_fiction
python auto_launcher.py
```

**"Phase 5 failed to initialize"**
```bash
mkdir -p memory_data
```

**"OpenAI API error"**
```bash
export OPENAI_API_KEY="your-key-here"
# Or create .env file
```

**"Memory contamination between stories"**
- Ensure you're using the updated code with per-story isolation
- Check that `memory_data/` contains timestamped subdirectories

**"Story quality issues"**
1. Increase novelty (0.7-0.9)
2. Enable Phase 5 with LLM analysis
3. Use more scenes (18-20)
4. Check staleness metrics

**"Arcs not closing"**
- Increase completion pressure
- Check arc urgency calculations
- Review scene evaluator feedback

**"Characters sound the same" (Phase 3.6)**
1. Check that prose_style is being generated in character config
2. Verify context_builder is injecting prose_style_directive FIRST
3. Ensure prose styles are diverse (no two characters share internal_thoughts_format)
4. Run `--voice-test` with extreme archetypes to verify system works
5. Check StalenessDetector.detect_prose_convergence() for voice collapse

### Useful Commands

```bash
# List all stories
python story_manager.py list

# Inspect Phase 5 data
python story_manager.py inspect memory_data/story_YYYYMMDD_HHMMSS

# Check API key
echo $OPENAI_API_KEY

# View latest output
cat outputs/phase35_narrative.txt

# Run voice differentiation test
python main_phase35.py --voice-test
```

---

## Appendix A: Glossary

| Term | Definition |
|------|------------|
| **Arc** | A story thread with beginning, middle, and end |
| **Consolidation** | Post-scene update of psychology/relationships |
| **H₀-H₅** | Hierarchical prompt layers |
| **Perturbation** | Narrative disruption to prevent stagnation |
| **Phase 3** | Director mode (structure only) |
| **Phase 3.5** | Hybrid mode (structure + psychology) |
| **Phase 3.6** | Voice differentiation mode (structure + psychology + distinct prose) |
| **Phase 5** | Memory & psychology subsystem |
| **ProseStyle** | 8-axis specification of character's prose voice |
| **Prose Convergence** | When character voices collapse toward house style |
| **Staleness** | Repetitive patterns across scenes |
| **Style Directive** | Example-driven instruction for character prose voice |
| **Tactic** | Narrative strategy (explore, escalate, etc.) |
| **Urgency** | Arc priority score (importance/scenes_remaining) |

---

## Appendix B: File Quick Reference

| File | Purpose |
|------|---------|
| `auto_launcher.py` | Main entry point (recommended) |
| `main_phase35.py` | Direct Phase 3.5/3.6 entry |
| `story_manager.py` | Story management utility |
| `agents/orchestrator_phase35.py` | Main orchestrator |
| `agents/character_agent.py` | Character representation |
| `agents/context_builder.py` | Prompt construction with style injection |
| `agents/staleness_detector.py` | Pattern + voice convergence detection |
| `agents/idea_generator.py` | Concept + prose style generation |
| `memory/phase5_engine.py` | Phase 5 main interface |
| `memory/vector_store.py` | Semantic memory |
| `memory/character_sheets.py` | CharacterSheet + ProseStyle models |
| `prompts/tactics.py` | Tactical guidance |
| `state/arc_manager.py` | Arc tracking |
| `config/character_config_voice_test.json` | Voice differentiation test archetypes |

---

## Appendix C: Version History

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | Nov 11, 2025 | Initial documentation |
| 2.0 | Nov 21, 2025 | Phase 3.5 integration, memory isolation, comprehensive rewrite |
| 3.0 | Nov 22, 2025 | **Phase 3.6: Prose-Level Voice Differentiation** - ProseStyle model, example-driven directives, prompt-start injection, anti-convergence monitoring |

---

## Appendix D: Phase 3.6 Quick Reference

### The Problem
All characters sound like "one author writing multiple characters" - same parenthetical thoughts, same sentence rhythms, same sensory focus.

### The Solution
1. **ProseStyle Model**: 8-axis specification per character
2. **Example-Driven Directives**: Concrete first-person POV examples, not abstract descriptions
3. **Prompt-Start Injection**: Style directive placed BEFORE character identity
4. **Diversity Enforcement**: No two characters share same internal_thoughts_format or sentence_complexity

### The Breakthrough
Abstract style description → Concrete first-person POV examples, injected before character identity.

### Key Files
- `memory/character_sheets.py`: ProseStyle model and to_style_directive()
- `agents/context_builder.py`: Prompt injection positioning
- `agents/idea_generator.py`: Prose style generation
- `agents/staleness_detector.py`: Voice convergence detection

### Verification
Run `python main_phase35.py --voice-test` with extreme archetypes to verify differentiation holds.

---

*End of UBERDOC 3.0*
