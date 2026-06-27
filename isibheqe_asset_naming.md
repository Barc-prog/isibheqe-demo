# Isibheqe demo — asset naming & save conventions

Purpose: a naming scheme for the **SVG glyphs** and **audio clips** so that when I hand you HTML, the `src` paths resolve to files you've actually produced — and so you make each asset *once*.

---

## Two anchoring principles

**1. Match your existing convention.** Your current site already names single-glyph files by *phonetic feature* — `Aspirated_bilabial_plosive.png`, `Voiceless_post-alveolar_fricative.png`. The new scheme extends that exact style rather than inventing a new one, so new assets sit alongside the old library and you don't relearn anything.

**2. Name by *content*, not by *position*.** A file is named for the sound or word it contains — never for the section/column it appears in. This is the important one, because the same sound recurs across sections, and content-naming means it's **one file referenced many times**. It also makes the script's politics literal: where two colonial spellings are the same sound, they resolve to the *same filename* — the file system itself collapses the orthographic divide.

---

## Why SVG, why mirrored folders

- **SVG, not PNG, for the new glyphs.** The sizing spec relies on fit-to-width scaling *and* inline tap-to-zoom. A raster PNG blurs when enlarged; SVG stays razor-sharp at any size, which is exactly what the zoom interaction needs. (Your existing PNGs still work as-is; SVG is the recommendation going forward.)
- **Glyph and audio mirror each other.** Same basename, different folder + extension. So from any glyph path the audio path is mechanically derivable — which keeps the HTML I write simple and predictable.

```
/assets/
  /glyphs/
    /cues/     Aspirated_bilabial_plosive_a.svg      ← single syllableblocks (hero tier)
    /words/    phapha.svg                            ← basic words (application tier)
  /audio/
    /cues/     Aspirated_bilabial_plosive_a.mp3
    /words/    phapha.mp3
```

Audio format: **.mp3** as the single universal format (your current site mixes .ogg/.mp3; standardising on mp3 is simpler). Add .ogg siblings later only if you want belt-and-braces fallback.

---

## Cue naming (hero tier — single syllableblocks)

**Rule:** `[Phonetic_feature_name]_[vowel].svg`, reusing your existing capitalised-underscored phonetic names, with the vowel appended.

- The vowel suffix is `a` for every cue in the current demo. It exists now so that when you build the apex primer (the i/e/o variants), those slot in as `_i`, `_e`, `_o` without renaming anything.
- Your existing PNGs are implicitly `_a` (the walkthrough confirms they're syllables on /a/). The new SVG set just makes the vowel explicit.

**The 24 unique cue assets** (29 sequence slots collapse to 24 — 5 are reuses):

| Canonical filename (`.svg` / `.mp3`) | Romanized | Appears in | Make once / reuse |
|---|---|---|---|
| Aspirated_bilabial_plosive_a | pha | Places, Modes 1 | make once, reuse 2× |
| Aspirated_dental_plosive_a | ṱa | Places | |
| Aspirated_alveolar_plosive_a | tha | Places, Manners 1, Modes 2 | make once, reuse 3× |
| Voiceless_palatal_plosive_a | tya | Places | |
| Aspirated_velar_plosive_a | kha | Places, Modes 3 | make once, reuse 2× |
| Voiceless_alveolar_fricative_a | sa | Manners 1 | |
| Aspirated_alveolar_affricate_a | tsa | Manners 1 | |
| Alveolar_trill_a | ra | Manners 1 | |
| Aspirated_alveolar_click_a | qha | Manners 1, Modes 4 | make once, reuse 2× |
| Voiced_alveolar_nasal_a | na | Manners 1 | |
| Alveolar_syllabic_trill_a | rra | Manners 1 | ⚑ creator |
| Voiced_palatal_nasal_a | nya | Manners 1 | |
| Voiceless_post-alveolar_fricative_a | sha / xa | Manners 2 | one glyph, two spellings ⚑ |
| Aspirated_post-alveolar_affricate_a | tsha | Manners 2 | |
| Retroflex_tap_a | la | Manners 2 | ⚑ creator |
| Voiced_bilabial_plosive_a | bha | Modes 1 | |
| Bilabial_ejective_stop_a | pa | Modes 1 | |
| Voiced_bilabial_implosive_a | ba | Modes 1 | |
| Voiced_alveolar_plosive_a | da | Modes 2 | |
| Alveolar_ejective_stop_a | ta | Modes 2 | |
| Voiced_velar_plosive_a | ga | Modes 3 | |
| Velar_ejective_stop_a | ka | Modes 3 | |
| Voiced_alveolar_click_a | gqa | Modes 4 | |
| Alveolar_click_a | qa | Modes 4 | tenuis, not ejective ⚑ |

---

## Word naming (application tier — basic words only)

**Rule:** lowercase the romanized word, **strip diacritics**, **strip any leading hyphen** (the stem marker — a filename must not begin with `-`), keep it ASCII.

- `-qhaqha` → `qhaqha.svg` · `-nyanya` → `nyanya.svg` (leading stem-hyphen dropped)
- `ṱaṱa` → diacritic stripped → `tata…` — **this collides** with `tata` (Xhosa "father", the /t/-ejective word). The single collision in the whole set. **Resolution rule:** *when stripping diacritics produces a duplicate, append the source-language code to both.* → `tata_ve` (Venda, dental) and `tata_xh` (Xhosa, ejective). Every other word is unique with no suffix needed, so you only ever think about this once.
- Reminder: only **basic** words get assets. Harder words (*iphupho, thothokiso, -thetha*…) are text-and-gloss only — no SVG, no audio.

**The ~26 basic-word assets** (reuses marked):

| Filename | Word | Section | Note |
|---|---|---|---|
| phapha | phapha | Places, Modes 1 | make once, reuse 2× |
| tata_ve | ṱaṱa | Places | dental; language-suffixed to avoid collision |
| thatha | thatha | Places, Manners 1, Modes 2 | make once, reuse 3× |
| itya | itya | Places | vowel-initial, multi-block |
| khokho | khokho | Places, Modes 3 | make once, reuse 2× |
| sapha | sapha | Manners 1 | isiXhosa, "to give / hand out" (instruction) — replaced earlier *kusasa* |
| tsatsa | tsatsa | Manners 1 | |
| rara | rara | Manners 1 | |
| qhaqha | -qhaqha | Manners 1 | hyphen stripped |
| nana | nana | Manners 1 | |
| rra | rra | Manners 1 | word; distinct from the cue file ⚑ |
| nyanya | -nyanya | Manners 1 | hyphen stripped |
| xava | xava | Manners 2 | |
| intsha | intsha | Manners 2 | |
| lala | lala | Manners 2 | |
| bhabha | bhabha | Modes 1 | |
| papadi | papadi | Modes 1 | 3 blocks (a-a-i) |
| baba | baba | Modes 1 | see baba/vava below ⚑ |
| vava | vava | Modes 1 | see baba/vava below ⚑ |
| idada | idada | Modes 2 | |
| tata_xh | tata | Modes 2 | ejective; language-suffixed |
| gogo | gogo | Modes 3 | |
| kuku | kuku | Modes 3 | |
| qhoqhoqho | qhoqhoqho | Modes 4 | 3 blocks |
| gqogqosha | gqogqosha | Modes 4 | 3 blocks (o-o-a) |
| qoqo | qoqo | Modes 4 | |

---

## Two cells awaiting the creator's call (affects asset count)

- **baba / vava** (Modes 1 implosive). If he confirms they're the *same syllabeme* (the decolonial collapse), they become **one** glyph asset with one filename. If the script faithfully distinguishes /ɓ/ (implosive) from /v/ (fricative) — my read — they stay **two** assets, `baba` and `vava`. Provisioned as two for now; trivial to merge if he says one.
- **sha / xa** (Manners 2 fricative). Treated as **one** glyph (one /ʃ/ sound, two colonial spellings) — `Voiceless_post-alveolar_fricative_a`. The on-page label shows both romanizations; the file is singular. Confirm this is the intended collapse.

---

## Production scope at a glance
- **~24 cue glyphs + ~24 cue audio** (hero tier)
- **~26 word glyphs + ~26 word audio** (application tier)
- ≈ **50 glyphs + 50 audio** total, before any baba/vava merge.
- The reuse markers mean several "slots" across sections cost you zero extra work — make *thatha* once, it serves three sections.

## Reader-facing footnotes to write (carry-over)
- Stem convention: most entries are verb **stems/roots**, not full words; hyphen marks where a prefix attaches.
- (If clicks get their own mode labels) a note on the click series' third column.
