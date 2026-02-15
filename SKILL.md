# Pet Psychic Hook Generator

Generate viral TikTok hooks from pet psychic reading screenshots.

## Quick Start

Upload a reading screenshot or paste the text, and I'll generate 3 hooks based on:
- Reading theme extraction
- Emotional tone detection  
- High-performing formulas from the database

## How to Use

**Example Request:**
```
"Generate hooks for this reading: My cat said she's been monitoring my water intake..."
```

**Response Format:**
```
Reading Theme: Health monitoring, protective behavior
Emotional Tone: Surprising, caring

Generated Hooks:
1. "My pet's been tracking my habits without me knowing 😳" (Secret Exposed)
2. "I didn't believe this until my pet revealed what they notice about me" (Skeptic Converted)
3. "My pet's reading exposed how much they actually pay attention" (The Judgment)

Suggested Visuals:
- Show water bottle with pet watching
- Split screen: you vs pet's perspective
- Text overlay: "They know..."
```

## Hook Formulas

1. **Relationship Dynamic** - "[Person] didn't believe until..."
2. **Secret Exposed** - "The reading revealed..."
3. **Emotional Reveal** - "[Rescue pet]'s past..."
4. **Relatable Humor** - "We asked what [pet] thinks about..."
5. **The Judgment** - "[Pet] judges me..."
6. **Bunny-Specific** - Chaos and world domination angles

## Hook Quality Principles

**Must Sound Natural:**
- Write like you'd actually say it in conversation
- Avoid awkward phrasing like "we submitted him" → use "then he saw this"
- No em dashes (--) that break the flow unnaturally

**Establish Stakes:**
- Why should the reader care?
- "My dad finally believes I'm not wasting my time" (low stakes)
- "My dad FREAKED out" (high stakes - reaction matters)

**Provide Context:**
- Explain what the app does clearly
- "This app" → "this pet psychic app"
- "Do her hamster" → "read her hamster's mind"

**Include Specific Details:**
- Generic: "She sent me the money"
- Specific: "It revealed something only she and her cat would know"
- The person in the hook should relate to the reading content

**Relationship Archetype Must Connect:**
- Landlord hooks work when reading is ABOUT landlord-related behavior
- Example: "My landlord didn't believe my rabbit was turning up the thermostat"
- NOT: "My landlord didn't believe rabbits had opinions" (why do we care?)

## Hook Database

**Location:** `hook-database.json`

Contains 19 hooks with ratings (1-10), usage tracking, and formula categories.

**Update ratings after posting:**
- 10 = Viral (100K+ views)
- 8-9 = Strong (10K+ views)
- 6-7 = Decent (1K+ views)
- Below 6 = Retire

## A/B Testing

Same reading, different hooks:
- Post Hook A → Wait 24h → Track engagement
- Post Hook B → Wait 24h → Track engagement
- Compare and update database

## Workflow

1. **Upload reading** (screenshot or text)
2. **Receive 3 hook options**
3. **Pick one or request variations**
4. **Get visual suggestions**
5. **Film with confidence**

---

*Last updated: 2026-02-14*
