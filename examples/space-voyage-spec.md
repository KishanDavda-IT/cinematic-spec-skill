# Build Prompt: VOID — Space Exploration Hero
A high-fidelity cinematic hero section for an aerospace pioneer, featuring glassmorphic UI elements over a deep-space nebula background.

## Tech Stack (pinned, CDN-only)
- React 18: `https://unpkg.com/react@18/umd/react.production.min.js`
- React DOM 18: `https://unpkg.com/react-dom@18/umd/react-dom.production.min.js`
- Framer Motion 11: `https://unpkg.com/framer-motion@11/dist/framer-motion.js`
- Tailwind CSS 3: `https://cdn.tailwindcss.com`
- Babel: `https://unpkg.com/@babel/standalone/babel.min.js`

## Fonts
- **Heading**: `Newsreader`, serif, italic. Import: `https://fonts.googleapis.com/css2?family=Newsreader:ital,opsz,wght@1,6..72,200..800&display=swap`
- **Body**: `Inter`, sans-serif. Import: `https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500&display=swap`

## Design System / Global Utilities
```css
@layer utilities {
  .glass-card {
    background: rgba(255, 255, 255, 0.03);
    border: 1px solid rgba(255, 255, 255, 0.08);
    backdrop-filter: blur(16px);
    -webkit-backdrop-filter: blur(16px);
  }
  .glass-pill {
    background: rgba(255, 255, 255, 0.05);
    border: 1px solid rgba(255, 255, 255, 0.12);
    backdrop-filter: blur(8px);
    -webkit-backdrop-filter: blur(8px);
  }
  .text-glow {
    text-shadow: 0 0 20px rgba(255, 255, 255, 0.15);
  }
}
```

## Page Sections

### 1. Hero Content Layer
**Background / Media**
- **Asset**: `https://images.unsplash.com/photo-1464802686167-b939a67a06d1?q=80&w=2070&auto=format&fit=crop` (Deep nebula)
- **Overlay**: `bg-black/60 absolute inset-0 z-0`
- **Animation**: `animate: { scale: [1.05, 1], opacity: [0, 1] }, transition: { duration: 2, ease: "easeOut" }`

**Layout Shell**
- `relative min-h-screen w-full bg-black text-white flex flex-col items-center justify-center overflow-hidden font-body px-6 text-center`

**Components (Top to Bottom)**

1. **Logo (Top Left)**
   - `fixed top-10 left-10 z-50`
   - `glass-pill w-12 h-12 flex items-center justify-center rounded-full italic font-serif text-xl` — `"a"`

2. **Top Badge**
   - `glass-pill px-2 py-1 flex items-center gap-3 mb-12`
   - Inner Pill: `bg-white text-black px-4 py-0.5 rounded-full font-bold text-xs` — `"New"`
   - Text: `text-xs tracking-wide font-light` — `"Maiden Crewed Voyage to Mars Arrives 2026"`
   - **Motion**: `initial: { y: -20, opacity: 0 }, animate: { y: 0, opacity: 1 }, transition: { duration: 0.8, delay: 0.2 }`

3. **Hero Title**
   - `font-serif italic text-5xl md:text-7xl lg:text-8xl leading-[1.1] max-w-4xl mb-8 tracking-tight text-glow`
   - Content: `"Venture Past Our Sky Across the Universe"`
   - **Motion**: `initial: { filter: 'blur(12px)', opacity: 0, scale: 1.1 }, animate: { filter: 'blur(0px)', opacity: 1, scale: 1 }, transition: { duration: 1, delay: 0.4 }`

4. **Hero Description**
   - `text-sm md:text-lg text-white/60 max-w-2xl mb-12 leading-relaxed font-light`
   - Content: `"Discover the universe in ways once unimaginable. Our pioneering vessels and breakthrough engineering bring deep-space exploration within reach—secure and extraordinary."`
   - **Motion**: `initial: { opacity: 0, y: 10 }, animate: { opacity: 1, y: 0 }, transition: { duration: 0.8, delay: 0.6 }`

5. **Actions (Buttons)**
   - `flex items-center gap-8 mb-20`
   - Primary: `glass-pill px-8 py-3 rounded-full flex items-center gap-3 font-medium transition-all hover:bg-white/10` — `"Start Your Voyage" + IconArrowUpRight`
   - Secondary: `flex items-center gap-2 text-sm font-medium hover:text-white/80 transition-colors` — `IconPlay + "View Liftoff"`
   - **Motion**: `initial: { opacity: 0 }, animate: { opacity: 1 }, transition: { duration: 0.8, delay: 0.8 }`

6. **Stats Grid**
   - `grid grid-cols-1 md:grid-cols-2 gap-6 max-w-3xl w-full mb-16`
   - Card Style: `glass-card p-8 rounded-3xl flex flex-col items-start text-left gap-10`
   - Card 1: 
     - Icon: `IconClock`
     - Value: `font-serif italic text-4xl` — `"34.5 Min"`
     - Label: `text-xs text-white/40 uppercase tracking-widest` — `"Average Videos Watch Time"`
   - Card 2:
     - Icon: `IconGlobe`
     - Value: `font-serif italic text-4xl` — `"2.8B+"`
     - Label: `text-xs text-white/40 uppercase tracking-widest` — `"Users Across the Globe"`
   - **Motion**: `initial: { opacity: 0, y: 20 }, animate: { opacity: 1, y: 0 }, transition: { duration: 0.8, delay: 1 }`

7. **Footer / Partners**
   - `flex flex-col items-center gap-6`
   - Label Badge: `glass-pill px-6 py-1 text-[10px] uppercase tracking-widest font-medium` — `"Collaborating with top aerospace pioneers globally"`
   - Partners List: `flex flex-wrap justify-center gap-x-12 gap-y-4 font-serif italic text-2xl text-white/80`
   - Brands: `"Aeon", "Vela", "Apex", "Orbit", "Zeno"`
   - **Motion**: `initial: { opacity: 0 }, animate: { opacity: 1 }, transition: { duration: 0.8, delay: 1.2 }`

## Icons (inline SVGs)

- **IconArrowUpRight**: `viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="2" strokeLinecap="round" strokeLinejoin="round"`
  - Path: `d="M7 17L17 7M7 7h10v10"`
- **IconPlay**: `viewBox="0 0 24 24" fill="currentColor"`
  - Path: `d="M8 5v14l11-7z"`
- **IconClock**: `viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="1.5"`
  - Path: `M12 8v4l3 3m6-3a9 9 0 11-18 0 9 9 0 0118 0z"`
- **IconGlobe**: `viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="1.5"`
  - Path: `M12 21a9 9 0 100-18 9 9 0 000 18zm0 0c2.485 0 4.5-4.03 4.5-9s-2.015-9-4.5-9-4.5 4.03-4.5 9 2.015 9 4.5 9zM3 12h18"`

## Notes
- Background uses a high-resolution Unsplash asset for nebula textures.
- Animation stagger is calculated based on element depth (top → bottom).
- Glassmorphism is achieved via `backdrop-filter: blur` and low-opacity white backgrounds.
- Text glow uses `text-shadow` for the cinematic serif headings.
