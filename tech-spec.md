# Tech Spec — NOVO PES 2026 Landing Page

## Dependencies

- Google Fonts: DM Serif Display (400, italic), Geist Mono (fallback: Space Mono from Google Fonts), Inter (300, 400)
- No external CSS/JS frameworks
- No build step required

## Component Inventory

### Layout
- **UrgencyBar**: Fixed top bar with pulse animation
- **HeroSection**: Full-height centered hero with radial glow
- **SocialProofBar**: 3-column stats band
- **PainSection**: 3-column pain point cards
- **SolutionSection**: 3-column solution cards
- **TestimonialsSection**: 3-column testimonial cards
- **CentralCTA**: CTA band with trust badges
- **FAQSection**: Accordion-style FAQ (5 items)
- **FinalCTA**: Centered CTA in glass card
- **Footer**: Minimal footer

### Reusable Components
- **GlassCard**: `backdrop-filter: blur(24px)`, rgba(255,255,255,0.02) background, 1px border
- **SilverButton**: Gradient button with hover lift + glow
- **SectionLabel**: Geist Mono uppercase label (repeated across sections)
- **SectionHeadline**: DM Serif Display italic headline
- **AnimateOnScroll**: Intersection Observer wrapper for slide-up animations

### Animations
- **slideUp**: CSS keyframe, 0.8s, cubic-bezier(0.16, 1, 0.3, 1)
- **staggerDelay**: CSS classes for 0.1s incremental delays
- **ScrollTrigger**: Intersection Observer (threshold 0.15)
- **FAQ toggle**: CSS height transition + chevron rotation
- **Urgency pulse**: CSS keyframe (scale 1.0 to 1.1, 2s infinite)

## Animation Implementation Table

| Animation | Library | Implementation | Complexity |
|---|---|---|---|
| Slide-up entrance | CSS keyframes + Intersection Observer | Native JS IO adds .animate class; CSS handles the transition | Low |
| Stagger delays | CSS classes | .delay-1 through .delay-4 classes with animation-delay | Low |
| FAQ accordion | CSS transition + JS toggle | JS toggles a class; CSS transitions max-height and opacity | Low |
| Urgency emoji pulse | CSS keyframes | @keyframes pulse with transform: scale | Low |
| Button hover glow | CSS transition | transition: all 0.3s ease on :hover | Low |

All animations are low-complexity CSS/JS native. No animation libraries needed.

## State & Logic Plan

### FAQ Accordion State
- Each FAQ item tracks open/closed state
- Only one item open at a time (accordion pattern)
- Toggle on click: close currently open, open clicked
- Use data attributes to link question and answer elements

### Scroll Animation Trigger
- Intersection Observer on each section
- When section enters viewport (threshold 0.15), add .animate-slide-up class
- Child elements get staggered delay classes (.delay-1, .delay-2, etc.)

### Mobile Menu (if needed)
- Not required; single page with scroll flow

## Other Key Decisions

- **Single HTML file**: All CSS in `<style>`, all JS in `<script>`
- **Font loading**: Google Fonts via `<link>` in head with display=swap
- **Geist Mono fallback**: Use Space Mono from Google Fonts if Geist Mono fails to load
- **Noise texture**: Inline SVG data URI, not external file
- **Avatar images**: Generated assets, referenced as external files (will be in same directory)
- **No localStorage/cookies needed**: Purely presentational landing page
- **CTA onclick**: Points to `#` as placeholder for payment link
