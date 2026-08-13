[README-draft-picker.md](https://github.com/user-attachments/files/31010936/README-draft-picker.md)
# Random Draft Picker — Edit Guide

This file explains **where to change things** in `draft-picker.html` so you don’t have to dig through the whole script.

All editable settings live near the **top of the `<script>` block** (search for `EDITABLE CONSTANTS`).

---

## 1. Master card list

```js
const MASTER_LIST = [
  "Mining",
  "Lumberjacking",
  "Blacksmith",
  // ...
  "Free Pick"
];
```

- Add or remove any card name (one string per entry).
- `"Free Pick"` is special: it stays in the pool and lets you choose any available card when it appears in **Generate 3**.
- It never appears in **Starter Draft**.

---

## 2. Prerequisites (skill gates)

```js
const PREREQS = {
  "Blacksmith":  ["Mining"],
  "Tinkering":   ["Mining"],
  "Carpentry":   ["Lumberjacking"],
  "Bowcraft":    ["Lumberjacking"],
};
```

- Format: `"CardThatIsLocked": ["RequiredCard1", "RequiredCard2"]`
- The locked card only enters the roll pool after you have **at least one** of the required cards in **Picked so far**.
- Cards listed here are also **weighted** (see below).

---

## 3. Weighted chance (prereq cards)

```js
const WEIGHTED_CHANCE = 0.15;  // 15%
```

- When a card has prerequisites **and** those prereqs are met, it only has this chance to appear in a roll.
- When it does appear, it gets a **golden glow** + “Weighted” badge.
- Examples: `0.05` = 5%, `0.25` = 25%, `1` = always (once unlocked).

---

## 4. Milestone reward slots

```js
const MAX_MILESTONE_SLOTS = 5;
```

- Maximum number of bank slots on the page.
- **Unlock rule:** slots come from **prestige only**
  - Prestige 0 → 0 slots  
  - Prestige 1 → 1 slot  
  - Prestige 2 → 2 slots  
  - …up to this max  
- Raise this number to allow more slots after higher prestiges.

**How to use slots in-game**
- Empty unlocked slot → bank a remaining card (removes it from the pool).
- Filled slot (✓) → claim it into **Picked so far**.

---

## 5. Starter Draft size

```js
const STARTER_COUNT = 4;
```

- How many cards **Starter Draft** shows at once.
- You can lock any of them, reroll the unlocked ones, then **Finalize**.

---

## 6. Experience & level formula

```js
const XP_BASE = 500;           // XP needed for level 1 → 2 at prestige 0
const PRESTIGE_GROWTH = 0.25;  // +25% XP cost per prestige
const LEVEL_GROWTH = 0.08;     // +8% XP cost per level within a prestige
```

**Formula**

```
XP to next level = XP_BASE × (1 + PRESTIGE_GROWTH × prestige) × (1 + LEVEL_GROWTH × (level − 1))
```

| Prestige | Level 1 | Level 10 | Level 50 |
|----------|---------|----------|----------|
| 0        | 500     | ~860     | ~2,460   |
| 1        | 625     | ~1,075   | ~3,075   |

- Levels go from **1 → 100**.
- **Total XP earned** is tracked under the bar.
- **Every 4 levels** → +1 **Generate charge** (does **not** unlock a milestone slot).

---

## 7. What each button does

| Button | Purpose |
|--------|---------|
| **Starter Draft** | Draw cards, lock some, reroll others, Finalize into Picked |
| **Generate 3 Cards** | Needs a Generate charge (from leveling). Pick 1 of 3. Optional per-card reroll (costs 1 reroll token) |
| **Manual Pick** | Add any available card straight to Picked |
| **Ban Cards** | Popup: full ban / starter-only / generate-only. ✕ to unban |
| **Custom Random** | Popup: type lines, pick one at random (not saved) |
| **Export / Import Save** | JSON file for sharing or backup |
| **Death Reset** | Soft reset: returns drafted cards to the pool. Keeps levels, prestige, milestones, bans, rerolls, generate charges |
| **Full Reset** | Wipes **everything** |
| **Prestige** | Appears at level 100. Soft-resets drafted cards, level → 1, +5 rerolls, +1 milestone slot (if under max) |

---

## 8. Status line

```
Remaining · Picked · Prestiged · Rerolls · Generate charges
```

- **Rerolls** — spent when you reroll a single Generate card, or when you reroll unlocked Starter cards (if you have tokens).
- **Generate charges** — earned every 4 levels; each Generate 3 uses one.

---

## 9. Bans (quick reference)

| Ban type | Effect |
|----------|--------|
| **Full** | Never appears anywhere |
| **Starter only** | Hidden from Starter Draft only |
| **Generate only** | Hidden from Generate 3 only |

Re-add anytime from the Ban popup (✕ on the tag).

---

## 10. Save data

- Auto-saved in the browser (`localStorage` key: `draftPickerState_v4`).
- **Export Save** downloads `draft-save.json` — keep it next to the HTML when sharing.
- **Import Save** loads that file back.

---

## Quick “I want to…” checklist

| Goal | What to edit |
|------|----------------|
| Add new skills/items | `MASTER_LIST` |
| Gate a skill behind another | `PREREQS` |
| Make weighted cards rarer/more common | `WEIGHTED_CHANCE` |
| Allow more bank slots after prestige | `MAX_MILESTONE_SLOTS` |
| Change Starter hand size | `STARTER_COUNT` |
| Change XP difficulty | `XP_BASE`, `LEVEL_GROWTH`, `PRESTIGE_GROWTH` |

After editing the HTML, refresh the page.  
If something looks wrong, try **Full Reset** once (or clear site data for the file) so old save shape doesn’t conflict.
