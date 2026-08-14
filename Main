# Random Draft Picker — Edit Guide

Single-file app: `draft-picker.html`. Open it in a browser. Progress saves in `localStorage` (export JSON to share).

---

## Where to edit (top of `<script>`)

| Constant | Purpose |
|----------|---------|
| `MASTER_LIST` | Skill cards + `"Free Pick"` |
| `PREREQS` | Skill gates, e.g. `"Blacksmith": ["Mining"]` |
| `ITEM_PACKS` | Named packs → list of items inside |
| `ITEM_LOOSE` | Standalone item entries (both packed & unpacked modes) |
| `WEIGHTED_CHANCE` | Chance for prereq-gated skills to appear (default `0.15`) |
| `MAX_MILESTONE_SLOTS` | Max bank slots (unlock 1 per prestige) |
| `STARTER_COUNT` | Cards shown in Starter Draft |
| `XP_BASE` / `PRESTIGE_GROWTH` / `LEVEL_GROWTH` | XP formula |

### XP formula

```
XP to next level = XP_BASE × (1 + PRESTIGE_GROWTH × prestige) × (1 + LEVEL_GROWTH × (level − 1))
```

### Adding a pack

```js
const ITEM_PACKS = {
  "All Swords": ["Katana", "Longsword", "Broadsword"],
  // "Your Pack Name": ["Item A", "Item B"],
};
```

- **Packed mode** (Modifiers): pool = pack names + `ITEM_LOOSE`. Rolling a pack unlocks that whole pack entry.
- **Unpacked mode**: pool = every item inside every pack + `ITEM_LOOSE`. Pack names are not rollable.

After changing packs, use **Modifiers → Apply / Refresh Rules** (or Full Reset on a clean test).

---

## Buttons (quick)

| Control | Role |
|---------|------|
| **Starter Draft** | Lock / unlock cards, reroll unlocked, Finalize into Picked |
| **Generate 3 Skills** | Costs 1 Generate charge; pick 1 of 3 (Confirm to lock) |
| **Generate 3 Items** | Same charges; only if Item Draft is enabled in Modifiers |
| **Manual Pick** | Add any available skill |
| **Ban Cards** | Full / Starter-only / Generate-only |
| **Modifiers** | Prereqs, interval, charges per award, max level, starter reroll cap, item mode |
| **Edit Values** (Tools) | Manually set charges, level, XP, rerolls, etc. |
| **Death Reset** | Return drafts to pool, restore charges & starter-reroll uses |
| **Full Reset** | Wipe everything |
| **Prestige** | At max level: soft-reset drafts, level 1, +5 rerolls, +1 milestone slot |

Generate charges come from leveling (every *N* levels, grant *M* charges — both set in Modifiers).

---

## Item packs (contents)

These are defined in `ITEM_PACKS` inside the HTML.

### Armor & gear

**All Bone Armors**  
Bone Arms, Bone Chest, Bone Gloves, Bone Helm, Bone Legs, Bone Skirt, Orc Helm, Skeletal Arms, Skeletal Chest, Skeletal Gloves, Skeletal Helm, Skeletal Legs

**All Chainmail Armors**  
Chainmail Coif, Chainmail Tunic, Chain Hatsuburi, Chain Leggings, Chain Skirt

**All Non-Set Helmets**  
Bascinet, Close Helm, Dread Helm, Helmet, Norse Helm, Oniwaban Hood

**All Footwear**  
Hiking Boots, Leather Boots, Oniwaban Boots, Royal Boots, Scaly Boots

**All Leather Armors**  
Female Leather Chest, Hide Tunic, Leather Leggings, Leather Arms, Leather Bustier, Leather Cap, Leather Chest, Leather Do, Leather Cloak, Leather Robe, Leather Gloves, Leather Gorget, Leather Haidate, Leather Hiro Sode, Leather Jingasa, Leather Legs, Leather Mempo, Leather Ninja Hood, Leather Ninja Jacket, Leather Ninja Mitts, Leather Ninja Pants, Leather Shorts, Leather Skirt, Leather Suneate, Oniwaban Gloves, Oniwaban Leggings, Oniwaban Tunic, Leather Shinobi Robe, Leather Shinobi Hood, Leather Shinobi Mask, Shinobi Cowl

**All Plate Armors**  
Plate Kabuto(Yellow), Female Plate Chest, Heavy Plate Jingasa, Light Plate Jingasa, Plate Arms, Plate Kabuto(Red), Plate Chest, Plate Do, Plate Gloves, Plate Gorget, Plate Haidate, Plate Hatsuburi, Plate Helm, Plate Hiro Sode, Plate Legs, Plate Mempo, Plate Skirt, Plate Suneate, Small Plate Jingasa, Plate Kabuto(Blue)

**All Ringmail Armors**  
Ringmail Arms, Ringmail Chest, Ringmail Gloves, Ringmail Legs, Ringmail Skirt

**All Royal Armors**  
Royal Arms, Royal Chest, Royal Gloves, Royal Gorget, Royal Helm, Royal Legs, Royal Shield

**All Scale Armor**  
Dragon Arms, Dragon Chest, Dragon Gloves, Dragon Helm, Dragon Legs, Drakbone Bracers, Drakbone Greaves, Drakbone Gauntlets, Drakbone Helm, Drakbone Tunic, Scaled Arms, Scaled Chest, Scaled Gloves, Scaled Gorget, Scaled Helm, Scaled Legs, Scaled Shield, Scalemail Shield, Scaly Arms, Scaly Chest, Scaly Gloves, Scaly Helm, Scaly Legs

**All Non-Set Shields**  
Bronze Shield, Buckler, Champion Shield, Chaos Shield, Crested Shield, Dark Shield, Elven Shield, Guardsman Shield, Heater Shield, Jeweled Shield, Metal Kite Shield, Metal Shield, Order Shield, Sun Shield, Virtue Shield, Wooden Kite Shield, Wooden Shield

**All Animal Hats**  
bearskin cap, deerskin cap, stagskin cap, wolfskin cap

**All Studded Armors**  
Female Studded Chest, Studded Arms, Studded Bustier, Studded Chest, Studded Do, Studded Gloves, Studded Gorget, Studded Haidate, Studded Hide Chest, Studded Huri Sode, Studded Legs, Studded Mempo, Studded Skirt, Studded Suneate

**All Wooden Armors**  
Wooden Legs, wooden gauntlets, wooden gorget, wooden arms, wooden tunic, wooden helm

### Weapons

**All Axes**  
Axe, Battle Axe, Double Axe, Executioner's Axe, Hatchet, Large Battle Axe, Ornate Axe, Two Handed Axe, War axe

**All Bows**  
Bow, Composite Bow, Crossbow, Elven Composite Longbow, Heavy Crossbow, Magical Shortbow, Repeating Crossbow

**All Knives**  
Assassin Dagger, Butcher Knife, Cleaver, Dagger, Large Knife, Leaf Blade, Throwing Dagger, War Cleaver

**All Maces**  
Club, Battle Mace, Hammerpick, Mace, Maul, Scepter, Spiked Club, War Hammer, War Mace, Whips, Wizard Wands, Smith Hammers(as weapons)

**All Special Range Weapons**  
Harpoon, Throwing Gloves, Wizard Staff

**All Oriental Weapons**  
Bokuto, Daisho, Kama, Lajatang, No Dachi, Nunchaku, Sai, Tekagi, Tessen, Tetsubo, Wakizashi, Yumi

**All Polearm Weapons**  
Bardiche, Halbred, Scythe

**All Forks and Spear Weapons**  
Bladed Staff, Double Bladed Staff, Pike, Trident, Pitchfork, Short spear, Spear, War fork

**All Staves**  
Black Staff, Quarter Staff, Gnarled Staff, Shepherd's Crook, Druid Staff

**All Swords**  
Bone Harvester, Broadsword, Claymore, Crescent Blade, Cutlass, Elven Machete, Elven Spellblade, Katana, Kryss, Lance, Longsword, Radiant Scimitar, Royal Sword, Rune blade, Scimitar, Short sword, sword, barbarian sword

### Loose items (`ITEM_LOOSE`)

Always in the item pool (packed and unpacked):  
Cloth Clothing, Jewelry and Trinkets, Quivers, Pugilist Gloves, Elixirs, Mixtures, Buff Potions, Damage Potions

---

## Saves

- Auto-save key: `draftPickerState_v6` (browser localStorage)
- **Export Save** → `draft-save.json`
- **Import Save** loads that file back
