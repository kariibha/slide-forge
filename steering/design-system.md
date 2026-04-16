# Deck Forge Design System — Public Edition

## Color Palettes

### Dark Mode (default)
```css
:root { --bg:#0F172A; --panel:rgba(30,41,59,0.7); --bdr:rgba(255,255,255,0.08);
        --accent:#818CF8; --accent2:#38BDF8; --green:#34D399; --red:#F87171;
        --yellow:#FBBF24; --text:#F1F5F9; --muted:#94A3B8; }
```
Background: `#0F172A` · Reveal theme: `black.css` · Bullet: `→` in accent

### Light Mode
```css
:root { --bg:#FFFFFF; --panel:rgba(241,245,249,0.9); --bdr:rgba(0,0,0,0.06);
        --accent:#4F46E5; --accent2:#0EA5E9; --green:#059669; --red:#DC2626;
        --yellow:#D97706; --text:#1E293B; --muted:#64748B; }
```
Background: `#FFFFFF` · Reveal theme: `white.css` · Bullet: `▸` in accent

## Required Base CSS

```css
.reveal .slides section { text-align:left; padding:28px 44px 44px 44px; box-sizing:border-box; overflow-y:auto; overflow-x:hidden; }
.reveal .slides section::-webkit-scrollbar { width:4px; }
.reveal .slides section::-webkit-scrollbar-thumb { background:rgba(255,255,255,0.12); border-radius:4px; }
.reveal h1 { font-size:1.8em; font-weight:800; line-height:1.1; letter-spacing:-0.03em; margin:0 0 4px 0; }
.reveal h2 { font-size:1.1em; font-weight:700; margin:0 0 6px 0; }
.reveal h3 { font-size:0.62em; font-weight:700; text-transform:uppercase; letter-spacing:0.04em; margin:0 0 5px 0; }
.reveal p, .reveal li { font-size:0.5em; line-height:1.45; margin:1px 0; }
.reveal ul { list-style:none; padding:0; margin:3px 0; }
.reveal ul li { padding:1.5px 0 1.5px 22px; position:relative; }
.reveal ul li::before { content:"→"; font-weight:700; position:absolute; left:4px; color:var(--muted); }
/* Glassmorphic cards */
.card { background:rgba(255,255,255,0.04); backdrop-filter:blur(20px) saturate(1.4); -webkit-backdrop-filter:blur(20px) saturate(1.4); border:1px solid rgba(255,255,255,0.1); border-radius:12px; padding:12px 16px; margin:3px 0; overflow:hidden; box-shadow:0 8px 32px rgba(0,0,0,.3), inset 0 1px 0 rgba(255,255,255,0.06); }
.g2 { display:grid; grid-template-columns:1fr 1fr; gap:8px; margin:5px 0; }
.g3 { display:grid; grid-template-columns:1fr 1fr 1fr; gap:7px; margin:5px 0; }
.g4 { display:grid; grid-template-columns:1fr 1fr 1fr 1fr; gap:7px; margin:5px 0; }
.callout { background:rgba(255,255,255,0.03); border:1px solid rgba(255,255,255,0.06); border-radius:10px; padding:8px 12px; margin:6px 0; text-align:center; }
.callout p { font-size:0.48em; margin:0; line-height:1.45; }
.tbl { width:100%; border-collapse:separate; border-spacing:0; font-size:0.4em; margin:5px 0; border-radius:8px; overflow:hidden; }
.tbl th { padding:6px 8px; text-align:left; font-weight:600; background:rgba(255,255,255,0.04); }
.tbl td { padding:5px 8px; vertical-align:top; }
.pill { padding:2px 8px; border-radius:14px; font-size:0.4em; font-weight:600; display:inline-block; margin:1px 2px; }
.sub { font-size:0.44em; margin:0 0 6px 0; color:var(--muted); }
.eyebrow { font-size:0.4em; font-weight:700; letter-spacing:0.12em; text-transform:uppercase; margin-bottom:3px; color:var(--accent); }
[contenteditable="true"]:focus { outline:2px solid rgba(129,140,248,0.5) !important; border-radius:4px; }
```

## Footer Bar

Every slide should have a footer. The footer content is customizable — ask the user for:
- Logo (SVG or image URL)
- Copyright text
- Company name

Default footer (no branding):
```css
.sf-footer { position:absolute; bottom:0; left:0; right:0; height:32px; background:rgba(0,0,0,0.4);
  display:flex; align-items:center; justify-content:space-between; padding:0 24px; z-index:100;
  border-top:1px solid rgba(255,255,255,0.04); }
.sf-footer span { font-size:10px; color:var(--muted); }
```

## Slide Sizing
- 1280×720, margin 0.02
- Max 6 bullets per card, max 5×5 tables
- Body text never below 0.5em
- Split slides rather than shrink fonts

## Reveal.js Config
```javascript
Reveal.initialize({
  width:1280, height:720, margin:0.02, scrollActivationWidth:null,
  hash:true, slideNumber:'c/t', transition:'fade', transitionSpeed:'fast',
  controls:true, progress:true, center:false,
  plugins:[RevealNotes]
});
```

**Important:** Do NOT use `view:'scroll'` — it breaks arrow navigation and speaker notes.

## Interactive Editing Toolbar

Every generated deck MUST include the editing toolbar. Press **E** to toggle.

### Required CSS
```css
.sf-toolbar { position:fixed; top:12px; right:12px; z-index:9999; display:none; flex-direction:column; gap:6px; background:rgba(0,0,0,0.85); backdrop-filter:blur(16px); border:1px solid rgba(255,255,255,0.1); border-radius:12px; padding:10px; box-shadow:0 8px 32px rgba(0,0,0,0.5); font-size:12px; color:#F1F5F9; }
.sf-toolbar.active { display:flex; }
.sf-toolbar-title { font-size:10px; font-weight:700; text-transform:uppercase; letter-spacing:0.1em; color:var(--accent,#818CF8); margin-bottom:2px; text-align:center; }
.sf-btn { display:flex; align-items:center; gap:6px; padding:6px 10px; border:1px solid rgba(255,255,255,0.08); border-radius:8px; background:rgba(255,255,255,0.04); color:#F1F5F9; cursor:pointer; font-size:11px; transition:all 0.15s; white-space:nowrap; }
.sf-btn:hover { background:rgba(255,255,255,0.1); border-color:rgba(255,255,255,0.2); }
.sf-btn-danger { border-color:rgba(248,113,113,0.2); }
.sf-btn-danger:hover { background:rgba(248,113,113,0.15); color:#F87171; }
.sf-btn-add { border-color:rgba(52,211,153,0.2); }
.sf-btn-add:hover { background:rgba(52,211,153,0.15); color:#34D399; }
.sf-divider { height:1px; background:rgba(255,255,255,0.08); margin:4px 0; }
.sf-card-selected { outline:2px solid rgba(129,140,248,0.6) !important; outline-offset:2px; }
.sf-edit-hint { position:fixed; bottom:44px; right:12px; z-index:9998; font-size:10px; color:rgba(255,255,255,0.4); pointer-events:none; }
```

### Required JavaScript
Same editing toolbar JS as the internal version — see the `design-system.md` in the internal power for the complete script. The only difference: new cards use `var(--accent)` colors instead of AWS orange.
