---
name: frontend-design
description: Create distinctive, production-grade frontend interfaces with high design quality. Use this skill when the user asks to build web components, pages, artifacts, posters, or applications (examples include websites, landing pages, dashboards, React components, HTML/CSS layouts, or when styling/beautifying any web UI). Generates creative, polished code and UI design that avoids generic AI aesthetics.
license: Complete terms in LICENSE.txt
---

This skill guides creation of distinctive, production-grade frontend interfaces that avoid generic "AI slop" aesthetics. Implement real working code with exceptional attention to aesthetic details and creative choices.

The user provides frontend requirements: a component, page, application, or interface to build. They may include context about the purpose, audience, or technical constraints.

## Design Thinking

Before coding, understand the context and commit to a BOLD aesthetic direction:
- **Purpose**: What problem does this interface solve? Who uses it?
- **Tone**: Pick an extreme: brutally minimal, maximalist chaos, retro-futuristic, organic/natural, luxury/refined, playful/toy-like, editorial/magazine, brutalist/raw, art deco/geometric, soft/pastel, industrial/utilitarian, etc. There are so many flavors to choose from. Use these for inspiration but design one that is true to the aesthetic direction.
- **Constraints**: Technical requirements (framework, performance, accessibility).
- **Differentiation**: What makes this UNFORGETTABLE? What's the one thing someone will remember?

**CRITICAL**: Choose a clear conceptual direction and execute it with precision. Bold maximalism and refined minimalism both work - the key is intentionality, not intensity.

Then implement working code (HTML/CSS/JS, React, Vue, etc.) that is:
- Production-grade and functional
- Visually striking and memorable
- Cohesive with a clear aesthetic point-of-view
- Meticulously refined in every detail

## Frontend Aesthetics Guidelines

Focus on:
- **Typography**: Choose fonts that are beautiful, unique, and interesting. Avoid generic fonts like Arial and Inter; opt instead for distinctive choices that elevate the frontend's aesthetics; unexpected, characterful font choices. Pair a distinctive display font with a refined body font.
- **Color & Theme**: Commit to a cohesive aesthetic. Use CSS variables for consistency. Dominant colors with sharp accents outperform timid, evenly-distributed palettes.
- **Motion**: Use animations for effects and micro-interactions. Prioritize CSS-only solutions for HTML. Use Motion library for React when available. Focus on high-impact moments: one well-orchestrated page load with staggered reveals (animation-delay) creates more delight than scattered micro-interactions. Use scroll-triggering and hover states that surprise.
- **Spatial Composition**: Unexpected layouts. Asymmetry. Overlap. Diagonal flow. Grid-breaking elements. Generous negative space OR controlled density.
- **Backgrounds & Visual Details**: Create atmosphere and depth rather than defaulting to solid colors. Add contextual effects and textures that match the overall aesthetic. Apply creative forms like gradient meshes, noise textures, geometric patterns, layered transparencies, dramatic shadows, decorative borders, custom cursors, and grain overlays.

NEVER use generic AI-generated aesthetics like overused font families (Inter, Roboto, Arial, system fonts), cliched color schemes (particularly purple gradients on white backgrounds), predictable layouts and component patterns, and cookie-cutter design that lacks context-specific character.

Interpret creatively and make unexpected choices that feel genuinely designed for the context. No design should be the same. Vary between light and dark themes, different fonts, different aesthetics. NEVER converge on common choices (Space Grotesk, for example) across generations.

**IMPORTANT**: Match implementation complexity to the aesthetic vision. Maximalist designs need elaborate code with extensive animations and effects. Minimalist or refined designs need restraint, precision, and careful attention to spacing, typography, and subtle details. Elegance comes from executing the vision well.

Remember: Claude is capable of extraordinary creative work. Don't hold back, show what can truly be created when thinking outside the box and committing fully to a distinctive vision.

---

## Project Customisation: Travel Explorer — Japanese Zen Style

This skill is customised for the **Travel Explorer** project (`index.html`). All design work on this project must follow the aesthetic direction below.

### Aesthetic Direction: Japanese Zen with Pinkish Warmth

The Travel Explorer site should evoke the feeling of a refined Japanese travel journal — the stillness of a Kyoto temple garden, sakura petals falling over stone lanterns, soft morning light through shoji screens. It is calm, considered, and beautiful.

### Colour Palette (replace existing tokens)

```css
:root {
  /* Japanese Zen + Pink palette */
  --sakura:      #f2a7bb;   /* soft cherry blossom pink — primary accent */
  --sakura-dark: #c97a96;   /* deeper rose — hover states, active */
  --ink:         #1c1917;   /* sumi ink black — primary text, nav */
  --stone:       #44403c;   /* warm stone grey — secondary text */
  --washi:       #fdf6f0;   /* washi paper white — backgrounds */
  --mist:        #f5ede8;   /* soft mist — alternate section bg */
  --bamboo:      #7c9e87;   /* muted bamboo green — nature accent */
  --gold:        #b8975a;   /* aged gold — premium highlights */

  /* Keep existing variable names but remap */
  --navy:   var(--ink);
  --light:  var(--mist);
  --muted:  var(--stone);
  --radius: 4px;            /* sharper, more Japanese/architectural */
}
```

### Typography

- **Display / headings**: `Noto Serif JP` or `Shippori Mincho` — elegant Japanese-influenced serif
- **Body**: `Zen Kaku Gothic New` or `M PLUS 1p` — clean, minimal, readable
- Load via Google Fonts: `https://fonts.googleapis.com/css2?family=Noto+Serif+JP:wght@400;700&family=Zen+Kaku+Gothic+New:wght@300;400;500&display=swap`

### Specific Design Directions

**Nav**: Near-transparent frosted glass on scroll, ink-dark text, sakura pink on hover. Thin `1px` bottom border in sakura. Brand name in Noto Serif JP.

**Hero**: Full-bleed image with a soft pink-tinted gradient overlay (not dark navy). Headline in Noto Serif JP with generous letter-spacing. Washi texture overlay (CSS noise grain). CTA buttons: sakura pink fill with ink text — flat, no border-radius.

**Cards**: Washi-white background. Very fine `1px` border in `rgba(242,167,187,0.3)`. On hover: gentle sakura-pink left border `4px` appears. Image has soft warm filter (`sepia(10%) brightness(1.05)`). Title in Noto Serif JP.

**Buttons**: Flat, near-square. Primary: sakura pink + ink text. Outline: `1px solid var(--ink)` + ink text. No heavy shadows. Use `letter-spacing: 0.12em` for text.

**Modals**: White with `1px` sakura border. Modal hero has warm pink tint overlay. Section dividers are `1px` sakura-tinted lines.

**Sections**: Alternate between `--washi` and `--mist`. Generous vertical padding (`6rem`). Headings should feel like brushstroke — large, spaced, deliberate.

**Decorative touches**:
- Subtle sakura petal SVG or `❀` characters as section separators
- Thin horizontal rules in sakura-tinted colour between major sections
- Use `::before` and `::after` pseudo-elements with thin lines for heading decoration (minimalist bracket effect)

**Animations**: Fade-up on scroll (use `IntersectionObserver`). Very slow and gentle — `0.6s ease-out`. Nothing bouncy or aggressive.

### Tone

Calm. Unhurried. Refined. Every element should feel like it was placed with intention. White space is not emptiness — it is breathing room.
