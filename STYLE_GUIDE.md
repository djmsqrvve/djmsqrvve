# DJMSQRVVE Style Guide: Twilight Shadowpunk

## Philosophy

Cyberpunk rebuilt with nature and community. Blade Runner meets Sleepywood.
Polished vibes without cringe. Confident, playful, evolved.

**Architecture**: Cyberpunk Wright // Inverted Googie Organic Forms
**Themes**: Neon-Deco, Googie-Atomic, Usonian-Luxe, Masquerave-Noir
**Motifs**: Corner Chevrons, Orbit Glows, Bioluminescent Tech

---

## Color Palette

### Primary Palette (extracted from approved YouTube assets)

| Swatch | Hex | Name | Usage |
|--------|-----|------|-------|
| Deep Night | `#120A12` | Near-black purple | Backgrounds, letterboxing, darkest shadows |
| Shadow Purple | `#1E121D` | Dark warm purple | Secondary backgrounds, dark UI panels |
| Twilight Indigo | `#322D5D` | Muted blue-purple | Mid-tone shadows, deep sky areas |
| Dusk Violet | `#552D68` | Rich purple | Primary sky mid-tone, atmospheric depth |
| Neon Magenta | `#A12766` | Vivid pink-magenta | Accent lighting, rim lights, highlights |
| Hot Bloom | `#C851B0` | Bright magenta-pink | Key accent color, neon glows, UI focus |
| Ember Red | `#A81C3C` | Deep crimson red | Character accents, weapon glows, alerts |
| Bioluminescent Teal | `#60ABD2` | Bright cyan-teal | Nature accents, bioluminescent elements |

### Extended Palette (from Rosé Pine dev theme)

| Swatch | Hex | Name | Usage |
|--------|-----|------|-------|
| Base | `#191724` | Deep purple-black | Code backgrounds, app chrome |
| Rose | `#ebbcba` | Warm pink | Primary text accent |
| Foam | `#9ccfd8` | Soft teal | Links, secondary accent |
| Gold | `#f6c177` | Warm amber | Highlights, warnings, warmth |

### Gradient Recipes

- **Twilight Sky**: `#552D68` -> `#A12766` -> `#C851B0` (top to bottom, vertical)
- **Shadowpunk Horizon**: `#1E121D` -> `#322D5D` -> `#60ABD2` (sky to ground, vertical)
- **Neon Accent**: `#A81C3C` -> `#C851B0` (linear, 45deg)

---

## Typography

### Recommended Fonts

| Font | Usage | Fallback |
|------|-------|----------|
| **Rajdhani** (Bold/SemiBold) | Thumbnail titles, video overlays, headers | Exo 2, Orbitron |
| **Inter** (Medium/SemiBold) | Body text, descriptions, metadata | Roboto, system-ui |
| **JetBrains Mono** | Code overlays, technical text, terminal | Fira Code, monospace |

### Text on Thumbnails

- **Title text**: Rajdhani Bold, 48-72px at 1280x720
- **Color**: White `#FFFFFF` with 2px `#120A12` stroke, or `#f6c177` (Gold) for emphasis
- **Drop shadow**: 4px offset, `#120A12` at 60% opacity
- **Position**: Right third of image (text-safe zone)
- **Max width**: 400px at 1280x720 (31% of frame width)

---

## Composition Rules

### YouTube Thumbnails (1280x720)

```
+------------------+------------+
|                  |            |
|   FOCAL POINT    |  TEXT-SAFE |
|   (character,    |    ZONE    |
|    scene,        |  (right    |
|    action)       |   third)   |
|                  |            |
+------------------+------------+
 <--- 67% --->      <-- 33% -->
```

- Character or focal element in **left two-thirds**, facing right
- Right third is **completely clear** for title text overlay
- **Strong rim/back lighting** on character for silhouette readability
- Background should have **depth layers** (foreground subject, midground environment, background sky)
- Must read clearly at **250px wide** (YouTube search result size)
- High contrast: works on both white AND dark YouTube backgrounds

### YouTube End Screen (1920x1080)

```
+-----------------------------------+
|                                   |
|           ATMOSPHERIC             |
|           BACKGROUND              |
|                                   |
|              +--------+  +------+ |
|              |SUGGEST- |  |SUB-  | |
|              |ED VIDEO |  |SCRIBE| |
|              +--------+  +------+ |
+-----------------------------------+
```

- Clean atmospheric gradient, no characters or focal elements
- **Lower-right quadrant** must be open for YouTube subscribe button + suggested video overlay
- **Center area** open for suggested video card
- Bioluminescent particles and subtle glow effects are ideal

### YouTube Channel Banner (2560x1440)

```
+-------+----------------------------+-------+
|       |                            |       |
|UNSAFE |    SAFE ZONE (1546x423)    |UNSAFE |
|       |   Channel name + tagline   |       |
|       |                            |       |
+-------+----------------------------+-------+
 <507px>  <----- 1546px ----->        <507px>
```

- **Device safe zone**: Center 1546x423 pixels visible on ALL devices
- Full 2560x1440 visible only on desktop
- Panoramic cityscape or wide environment compositions work best
- Central focal point with clear space for channel name text overlay
- No critical elements outside the center 1546x423 band

---

## Prompt Engineering Notes

### Effective prompt patterns for Leonardo Phoenix

1. **Always specify**: "no text, no UI elements" to prevent hallucinated text
2. **Brightness**: Include "vivid saturated colors, bright and punchy color grading, extremely high contrast" — Leonardo defaults dark
3. **Composition control**: Be explicit about zones — "completely empty right third for title text"
4. **Lighting**: "dramatic backlit character with strong rim lighting" produces the best silhouette readability
5. **Environment**: "luminous architecture" and "bioluminescent" keywords produce the signature teal accent glow
6. **Negative prompt essentials**: "text, watermark, UI overlay, blurry, low contrast, dark muddy image, underexposed, dim, desaturated"

### Aspect ratios in Leonardo

Leonardo's web UI uses preset radio buttons, not custom pixel dimensions:
- **16:9** → outputs 1344x768 (not exact 1280x720)
- **1:1** → outputs 1024x1024
- For YouTube thumbnails (1280x720): generate at 16:9, resize to 1280x720
- For channel banners (2560x1440): generate at 16:9, upscale 2x to 2688x1536, crop to 2560x1440

---

## Asset Pipeline

1. **Generate**: `PYTHONPATH=src venv/bin/python -m main generate-browser <prompt_key> --headless`
2. **Review**: `PYTHONPATH=src venv/bin/python -m main gallery` (localhost:6868)
3. **Rate**: 1-5 stars in gallery UI, favorite the approved ones
4. **Sync**: `PYTHONPATH=src venv/bin/python -m main sync --favorites --category youtube`
5. **Deliver**: Approved thumbnail path → Skivii Tools agent for YouTube upload
