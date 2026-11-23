
Build a single self-contained file `index.html` (inline CSS/JS, no build step, no backend, Google Fonts allowed). It's a whimsical, mobile-first Secret Santa app for my family. It must look delightful on an iPhone opened from an iMessage link.

**Theme:** "Hoffman-Imperial Construction Co. — Secret Santa Home Tools Edition, 2026." Gifts must be a home tool, spend up to **$100**.

**Participants and households (spouses must NOT draw each other; nobody draws themselves):**
- Nick Hoffman & Lisa Hoffman (parents) — Atlanta, GA
- John Hoffman & Sydney Hoffman — Mill Valley, CA
- Anna Imperial & Jonathan Imperial — Atlanta, GA

**Mascots:** Charlie (John & Sydney's son) and Effie (Anna & Jonathan's daughter), both about 1.5 years old, are the company's "Junior Site Foremen." Draw them as cute inline-SVG toddlers in oversized hard hats and tiny safety vests (Charlie with a little hammer, Effie with a clipboard). They don't give or receive gifts.

### Two modes, chosen by URL
1. **Organizer mode** (no `?t=` param): a "Foreman's Office" screen with a big "Draw Names" button.
   - Generate the assignment with constraint-respecting randomization. Prefer a **single 6-person loop** (A→B→C→D→E→F→A) so there are no mutual pairs; fall back to any valid derangement. Use `crypto.getRandomValues`.
   - **Do NOT display the pairings.** For each giver, show a card: "Nick's work order" with **Copy link** and **Text it** buttons (`sms:&body=` prefilled with a fun message plus the link). Also include a "Copy all as text" option that lists `Name: link` lines.
   - Each token encodes giver + receiver, obfuscated so it isn't human-readable: JSON → XOR with a fixed key plus a random salt → base64url. Links are `${location.origin}${location.pathname}?t=TOKEN`.
   - Add a small note: "Draw once, send once. Redrawing makes new links and old ones still work, so only send one set."
2. **Reveal mode** (`?t=` present): decode the token. If it's invalid, show a cheeky "This work order got lost in the drywall" screen.
   - **Gate:** "This work order is for **Nick**. Are you Nick?" with a big button "Yep, hard hat on 👷" so a curious spouse doesn't peek by accident.
   - **Animation sequence (about 8–10s, tap to skip, with a replay button), CSS/SVG plus light JS, no heavy libs (canvas confetti hand-rolled or `canvas-confetti` from cdnjs):**
     1. Snowy night construction site with a little house frame, string lights, and a crane with a wreath on its hook.
     2. Charlie and Effie wobble in from opposite sides, bonk hard hats, and giggle (bouncy easing).
     3. A red toolbox drops from the crane, lands with a squash-and-stretch, rattles, and bursts open. Tools tumble out (wrench, level, paintbrush, candy-cane screwdriver).
     4. A blueprint unrolls. "SECRET SANTA ASSIGNMENT" types out in blueprint lettering, then a big red rubber stamp slams down: **"APPROVED: you're building joy for ANNA"**. Screen shake, confetti of tiny nails, bolts and snowflakes.
     5. Effie holds up her clipboard; Charlie bangs his hammer.
   - Respect `prefers-reduced-motion` (show the final state with a fade).
   - **After the reveal, a "Work Order Details" card shows:**
     - Budget: up to $100. Theme: a home tool.
     - **The Site Inspection Code** (house rules): "No clutter. No single-use gadgets. If it doesn't earn its drawer space, it doesn't pass inspection."
     - **"Spark Some Ideas" carousel:** idea cards that rotate with a "Show me another blueprint" button, gently flavored by who they drew (see below). Framing is strictly *inspiration, not instructions*. Header copy along the lines of "Just a few sparks to get the gears turning — you know them best!" Never say "you should get" or "recommended," and never label or star any idea.
     - A "Screenshot this!" reminder, since the link holds the secret.

### Idea pools (fun flavor to bring the theme to life, not prescriptions)
Each idea gets a playful one-line pitch and a rough price, all under $100. Skip the obvious stud finder, drill and tape measure. Mix in a variety of:
- Clever first-time-homeowner **gadgets and tools** of the kind popular home blogs and "things I wish I'd bought sooner" lists rave about. Examples: a rechargeable motion-sensor puck light for closets and under cabinets; a magnetic wristband for holding screws; a compact cordless electric screwdriver (e.g. the Fanttik/HOTO style); a laser level for hanging gallery walls; a drain snake for clogs; Command-strip-style picture-hanging kits; a smart plug or smart button; a cordless handheld vacuum that hangs on the wall; a sleek wall-mounted pegboard or tool rail; a moisture meter; an under-sink organizer; a quality step stool that folds flat; a label maker for breaker panels.
- **Services and experiences** (handyman hours, cleanings, a pro walkthrough).
- **Consumables and upgrades** (filters, a great version of something they already have).
- **Smart-home helpers** with zero footprint.

The family vibe is anti-clutter, so the playful copy can wink at that ("earns its drawer space"), but never lecture. Flavor each person's pool a little by household:

- **For Nick or Lisa (Atlanta, already have plenty, in purge mode):** tilt toward zero-space and declutter-friendly sparks, mixed with a few genuinely great gadgets. Examples: a few hours from a professional organizer; a junk-haul or donation pickup booking; a "Purge Party" kit (one roll of premium contractor bags plus prepaid donation drop-off plus a coupon from the giver for 3 hours of hands-on help); a scanning service that digitizes old photo boxes; a pro knife-sharpening service; gutter cleaning or pressure-washing off the spring pollen; a "one in, two out" upgrade, e.g. a single excellent tool that replaces a drawer of mediocre ones, as long as two old items get donated.
- **For John, Sydney, Anna or Jonathan (first-time homeowners, minimalists who hate clutter and single-use items):** a mix of the gadget list above plus "year-one homeowner" sparks. Light city touches only (Mill Valley: hillside yard, damp foggy mornings; Atlanta: humidity, spring pollen), and **no disaster-prep ideas** (no earthquake or wildfire kits). Examples:
  - A "Meet Your House" session: a handyman or home inspector walks the house, labels every shutoff valve, breaker and filter size, and leaves a one-page house cheat sheet taped inside the panel door.
  - A first-year maintenance subscription: a year of the right-size HVAC filters auto-delivered, so the reminder is the gift.
  - Smart water-leak sensors under the sinks, water heater and washer (invisible, and they prevent the most expensive first-year surprise).
  - A 2-hour handyman or TaskRabbit credit for the "we'll hang that someday" list: art, curtain rods, the wobbly door.
  - A dryer-vent cleaning plus a gutter clean, the two chores new owners never know about.
  - Toddler-proofing done right: furniture anti-tip anchors installed, plus a pro babyproofing walkthrough (Charlie and Effie are climbing everything).
  - One heirloom-quality tool that replaces a junk drawer, e.g. a premium compact ratcheting multi-bit driver with a magnetic wall mount (it lives on the wall, not in a drawer).
  - A smart thermostat or smart lock install (useful every day, zero footprint).
  - Paint-swatch-to-wall: a credit for sample pots plus an hour of a painter's time to do the one accent wall they keep talking about.
  - City flavor: an Atlanta-house pollen pressure-wash, or a Mill Valley hillside yard cleanup or drip-irrigation tune-up.

Each pool should have about 12–15 ideas, shuffled so every reveal feels fresh. Do not badge, star, rank or mark any idea.

### Design direction
- Palette: construction-yellow, blueprint blue, candy-cane red, snowy white, warm string-light glow. Fonts: a chunky stencil/display font (e.g. "Black Ops One" or "Bungee") for headlines and a friendly rounded body font (e.g. "Nunito").
- Textures: blueprint grid background, hazard-tape borders on cards, snowfall layer.
- Microcopy is playful and construction-pun heavy ("Nailed it," "You've been drafted," "Permit granted," "Under budget, over the moon").
- Accessible: real buttons, good contrast, the name readable as text (not only in SVG).
- Works offline once loaded; no tracking; nothing saved server-side.

### Acceptance checks (do these before finishing)
- Run the draw logic 10,000 times in a quick Node test: no self-matches, no spouse matches, every person gives exactly once and receives exactly once, and loop mode succeeds.
- The token round-trips correctly and isn't readable by eye.
- Open the page in a browser at phone width (375px): organizer mode, a reveal link, and an invalid token all render, and the animation plays and can be skipped.

