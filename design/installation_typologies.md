# Installation Typologies — Active Corridors, Detmerode Pilot
## Wolfsburg Active Corridor Network — Design Document

**Status:** Design phase — Detmerode corridor  
**Date:** 2026-05-06  
**Scope:** Six typologies covering all five route segments

---

## Type System Overview

Six distinct installation types, deployed across the Detmerode → Porschestrasse corridor. Each type is matched to a specific route condition — spatial character, ambient light, degree of enclosure, and the cognitive task the user needs at that moment.

| Type | Name | Primary Function | Trigger |
|---|---|---|---|
| **A** | Wayfinding Post | Direction + distance + social proof | IR thermal · 4m |
| **B** | Threshold Marker | Journey gateway moment | LiDAR · 8m |
| **C** | Path Pulse | Moving light in enclosed corridor | Networked LiDAR |
| **D** | Narrative Post | Progress + historical audio | LiDAR · 3m |
| **E** | Cultural Panel | Permanent historical overlay | Passive (photocell dim) |
| **F** | Arrival Counter | Social proof at destination | LiDAR · 6m |

All types share three principles:
1. No camera data, no identity — LiDAR and IR thermal only
2. Edge processing — raw sensor data never leaves the node
3. Anonymous aggregate only — no individual trajectories stored

---

## Type A — Wayfinding Post

### Role
The primary legibility object. Creates a readable hierarchy of pedestrian paths across open areas with multiple competing routes. Deployed at junctions where the correct path is not self-evident. The post makes the city readable on foot for the first time.

### Context
Open modernist housing estates (Detmerode, Westhagen) where wide gaps between towers and multiple undifferentiated paths create decision fatigue. Also used in the Westhagen through-zone where construction activity disrupts the visual corridor.

### Physical Form
- **Height:** 1,200mm to top of cap
- **Section:** 60 × 60mm square post, tapered to 40mm at base plate
- **Material:** Weathering steel (Corten A / EN 10025-5). Allowed to develop natural patina — integrates with ground plane without requiring maintenance painting
- **Base plate:** 300 × 300 × 10mm Corten, flush-mounted to path surface. Four M12 anchor bolts to concrete pad below
- **Cap:** Cast aluminium housing, dark grey powder coat. Houses IR thermal sensor, solar cell, and antenna

### Content Layer
- **Display:** 200 × 130mm e-ink panel, flush to post face, IP67. Readable in direct sunlight. Updated on approach
- **Display content:** Direction arrow (fixed, north-facing for Porschestrasse route) / Distance to Porschestrasse (static, location-dependent) / Daily footfall counter (updated every 30 min via LoRa)
- **Base lighting:** 12 × 3W LED, 3,000K, embedded in base plate facing downward. Creates a warm ground pool (500mm radius). Not a task-lighting level — presence, not illumination

### Technology
- **Sensor:** Passive IR thermal, 90° field, 4m detection radius. Horizontal mounting in cap faces path approach
- **Processing:** ARM Cortex-M4 edge node in cap housing. Processes presence vector, discards immediately. Increments aggregate counter
- **Power:** 20W monocrystalline solar cell in cap top + 10,000mAh LiPo battery. 5-day autonomy in overcast conditions
- **Network:** LoRa 868MHz for aggregate counter sync. No real-time data transmission

### Response Behaviour
1. User enters 4m radius → LED base pool activates (100ms ramp)
2. E-ink panel refreshes with current distance + counter (1.2s refresh cycle)
3. LED holds for 30s after last presence detection, then ramps down over 10s
4. Display remains static between visits (e-ink holds last state, zero power)

### Quantity on Route
- Segment 1 (Estate): 4 units — 3 path junctions + 1 origin node at Detmerode start
- Segment 4 (Westhagen): 2 units — forest exit + mid-zone junction
- Segment 5 (City): 5 units — countdown series at 10, 7, 4, 2 min intervals

**Total: 11 units**

---

## Type B — Threshold Marker

### Role
Creates a deliberate experiential threshold — a moment the user consciously crosses. Transforms an infrastructure crossing into the start of a journey. The installation makes the user feel they have entered a different system, not just continued walking.

### Context
The Zusammenrücken Bridge (Braunschweiger Straße crossing). Potentially also at major district boundary crossings if the route network extends beyond Detmerode. Requires a physically compressed crossing point — a gateway.

### Physical Form
- **Configuration:** Paired pylons, one on each path edge, 4m span across standard path width
- **Pylon height:** 800mm (waist height — present without dominating)
- **Pylon section:** 80 × 80mm square hollow steel, 4mm wall thickness
- **Material:** Dark powder-coated mild steel, RAL 7021 (near black). Intentionally severe against the bridge's concrete and steel — not mimicking nature
- **LED strip:** 600mm × 20mm recessed channel on inner face of each pylon, warm white 3,000K, 500 lm/m. Faces across the path — lights the path surface, not the user
- **Audio emitter:** Directional speaker embedded in pylon base, angled 30° downward into the path. Frequency-optimised for the speech register (300Hz–3,400Hz) against traffic noise

### Content Layer
- **Audio:** A single low tone (220Hz, 0.8s duration) on user approach. Not a sound effect — closer to a breath. Then, at bridge entry marker only: embedded passive panel with name + message (see Type E for panel spec)
- **LED behaviour:** Sequential activation left-to-right (approach direction) over 1.5s. Not a flash — a pulse moving across the path, then held at 40% for 30s

### Technology
- **Sensor:** LiDAR (solid-state, 360° reduced to 90° FOV), shared between pair via CAN bus. 8m approach detection zone. Mounted flush in pylon cap
- **Processing:** Edge node shared by pair, mounted in left pylon base. Processes approach vector, triggers response sequence
- **Power:** Mains (bridge-adjacent infrastructure). 230V to 24V DC converter in base. Bridge has existing electrical infrastructure from lighting
- **Connectivity:** Ethernet to bridge electrical box. Aggregate presence data logged locally, purged daily

### Response Behaviour
1. User enters 8m zone → Audio tone triggers (single instance per approach, not on exit)
2. User enters 3m → LED sequence activates (L→R across path, 1.5s)
3. LEDs hold at 40% for 45s, then ramp to 15% ambient hold
4. System resets to ambient hold after 60s of no presence

### Quantity on Route
- Segment 2 (Bridge): 2 units (one pair at bridge entry, one pair at bridge exit into forest)

**Total: 2 pairs (4 pylons)**

---

## Type C — Path Pulse

### Role
Makes the user the centre of a moving pool of light. Solves the specific problem of enclosed low-light corridors — not by lighting the space, but by lighting the path immediately ahead and behind the user. The effect is privacy and forward motion simultaneously.

### Context
Rothehofer Forst. A protected conservation landscape with no existing lighting infrastructure. Any lighting must be minimal in ecological footprint, zero upward light pollution, and non-disruptive to nocturnal wildlife. The path is a former planning boundary — the installation should feel like a natural response, not urban infrastructure imposed on a landscape.

### Physical Form
- **Fixture:** Circular in-ground unit, 100mm diameter, 18mm proud of path surface (flush to within ±2mm)
- **Lens:** 6mm tempered borosilicate glass, matte finish. Anti-slip rating R11
- **Body:** Die-cast aluminium, black anodised. IP68 rated (1m submersion, 30 min)
- **LED:** Single 3W COB, 3,000K, 80° beam angle. 120 lm output. Warm, not clinical
- **Spacing:** Every 6m along path edge. Staggered left/right where path width permits (>2m)
- **Positioning:** Set into path edge surfacing, not centre of path. Sightline from walking direction — user sees glow, not source

### Technology
- **Sensor:** Corridor master node (Type D or standalone post) provides user position via LiDAR. Fixtures are slaves on a 12V DC RS-485 network
- **Controller:** Each fixture has a microcontroller receiving commands from master. No local sensing — pure response to network position signal
- **Activation logic:** User position P → fixtures within 40m ahead of P = active; fixtures within 40m behind P = fading (5s linear ramp off); all others = off
- **Power:** Low-voltage cable from corridor solar/battery controller. Master node manages power budget
- **Network:** RS-485 daisy chain, 9,600 baud. Position update every 500ms. Fixtures respond within 50ms

### Response Behaviour
- Creates an 80m illuminated corridor moving with the user at walking speed (~1.4m/s → fixture activations at ~4s intervals)
- At standstill, pool holds at current position
- If user turns back, pool reverses
- No fixtures light before user arrives — the light is always ahead, never static
- Ecological note: zero upward spill (downward-only lens), 3,000K (amber-warm, less disruptive to nocturnal insects than 4,000K+)

### Quantity on Route
- Segment 3 (Rothehofer Forst): approx 110m of path, one side = ~18 fixtures

**Total: 18 units** (plus 1 corridor master/controller node)

---

## Type D — Narrative Post

### Role
The midpoint witness. Delivers a progress update — you are halfway — and pairs it with a spoken historical account of the landscape the user is passing through. The audio is not decoration. It reframes the forest as designed separation rather than natural obstacle, making the act of crossing it feel consequential.

### Context
Forest midpoint in Rothehofer Forst — the moment the user is most isolated from urban cues. Also applicable at any site where cultural or historical content can reframe a transit space. Requires dwell potential — the user must be able to stop.

### Physical Form
- **Height:** 1,500mm to speaker grille
- **Section:** 100 × 100mm, octagonal chamfered profile (avoids square industrial look in natural setting)
- **Material:** Douglas fir or Larch, FSC-certified. Pre-treated with linseed oil + iron sulphate (grey-black weathering, no paint, integrates with forest floor palette). Post-set into ground 600mm via concrete plinth — no visible base
- **E-ink panel:** 250 × 180mm, IP67, flush to post face. Recessed 3mm into timber reveal. Held in black anodised aluminium bezel
- **Speaker:** 100mm full-range driver in a downward-facing conical housing at top. Protected by 316 stainless mesh. Horn geometry directs sound into a 2m radius at 1.5m below — audible within that zone, inaudible 5m away
- **LiDAR mount:** Flush cylindrical housing at 800mm height, facing path approach

### Content Layer
- **Display:** Progress text — "Halfway. You have walked 1.9 km. 19 minutes to Porschestrasse." Updates for cycling pace automatically
- **Audio:** Spoken narrative, calm voice, 45s. Triggers once per approach event. Content:
  > *"This forest was planned as a boundary. In the 1960s, Wolfsburg's districts were built to be self-contained. Detmerode on one side. Westhagen on the other. The bridge you just crossed didn't exist until 2021. You are walking a route that wasn't possible three years ago."*
- Audio content loaded locally (onboard storage). Updated via SD card / USB service port at base of post

### Technology
- **Sensor:** Solid-state LiDAR, 3m radius trigger zone
- **Display power:** E-ink draws power only on refresh (triggered by approach). Zero power between visits
- **Audio power:** Class-D amplifier, 5W peak. Activates only on trigger
- **System power:** 30W solar cell (mounted in a separate 300 × 400mm ground-level stainless tray, 2m from post — no visual intrusion on post itself) + 20,000mAh LiPo
- **Session logic:** Audio plays once per approach event. If user leaves and re-enters within 3 minutes, audio does not repeat (prevents loop annoyance for slow walkers)

### Response Behaviour
1. User enters 3m radius → Display refreshes with progress data
2. User slows or stops within 2m (velocity < 0.5m/s) → Audio triggers after 1.5s delay
3. Audio plays full 45s even if user moves away after 10s
4. Post returns to standby after 90s of no presence

### Quantity on Route
- Segment 3 (Forest): 1 unit at midpoint (1.9 km from Detmerode origin)

**Total: 1 unit**

---

## Type E — Cultural Panel

### Role
Makes the hidden visible. Points to what is already there — not new content, but existing content made legible. Every panel is site-specific. The text is about the specific building, object, or landscape feature it stands beside — not generic Wolfsburg history. Passive by design: no sensors, no interaction, permanent.

### Context
Wherever the route passes an object with a story that reframes the experience of walking. On the Detmerode corridor: Stephanuskirche (Alvar Aalto, 1963–68), Don Camillo and Peppone towers, the Rothehofer Forst boundary, Mittellandkanal, Westhagen renewal. Each panel is unique.

### Physical Form
- **Panel face:** 600 × 400mm (landscape) or 400 × 600mm (portrait, site-dependent). Nominal size — varies per site
- **Material:** 3mm etched stainless steel, grade 316, satin finish. Text chemically etched to 0.8mm depth — permanent, not printed, not painted
- **Backplate:** 3mm aluminium substrate, bonded to stainless face. Houses LED edge strip
- **LED edge:** 8mm LED strip, 3,000K, 300 lm/m, running around perimeter behind a 10mm reveal gap. Creates a warm outline glow — not a flood, a presence
- **Mounting:** Site-dependent. Wall-mount bracket (powder-coated black, 4× M8 fixings) or freestanding welded steel post, 50mm diameter, 1,000mm height. Post set in 400mm concrete collar

### Content
- Etched text: 2–4 short paragraphs. No more than 80 words total. Written in English and German
- QR code: etched directly into panel (permanent), links to AR companion app for extended content. Top right corner, 40 × 40mm
- No digital display, no electronic content on panel face — all content is permanent physical

### Technology
- **Sensor:** None. No presence detection
- **Lighting:** LED edge strip controlled by photocell (ambient light sensor, 20mm diameter, mounted discreetly on bracket)
- **Dimming:** 60% intensity at night (dusk to dawn), 15% in daylight, 0% in bright direct sun
- **Power:** Low-voltage mains (230V to 12V, cable buried under path surfacing) or solar panel (40W, attached to freestanding post base) + 6,000mAh LiPo for 3-day autonomy

### Variants
- **E1 — Wall-mounted:** For panels beside existing structures (Stephanuskirche, towers)
- **E2 — Freestanding:** For open-ground positions (forest boundary, canal path)

### Quantity on Route
- Segment 1: 1 unit (Stephanuskirche); 1 unit (Don Camillo/Peppone towers)
- Segment 3: 1 unit (Rothehofer Forst boundary — the designed separation story)
- Segment 4: 1 unit (Westhagen renewal — the parallel story)

**Total: 4 units** (2× E1 wall-mounted, 2× E2 freestanding)

---

## Type F — Arrival Counter

### Role
The final witness. Acknowledges that the user arrived on foot or by bike. The number — today's aggregate footfall — is social proof: this choice is not solitary. The act of arriving is made legible. The installation should feel like a civic statement, not a technology product.

### Context
Porschestrasse entry point — the moment the pedestrian or cyclist transitions from the corridor into the city centre. Scale and presence must be appropriate for the urban density here: larger, more prominent, more social.

### Physical Form
- **Option 1 — Plinth:** 500 × 200mm footprint, 900mm tall. Poured concrete base with embedded display module. E-ink display face 500 × 350mm, portrait orientation. LED border 25mm wide, around display perimeter. Dark powder-coated aluminium surround
- **Option 2 — Integration:** Counter display and LED border integrated into existing street furniture (bus shelter panel, existing signage frame). Form TBD based on site survey
- **Display content (always visible):** Large counter number (central, 60pt equivalent weight) / "people walked or cycled from the districts to the centre today" (beneath counter, smaller) / "You are one of them." (final line, amber)
- **Language:** German/English bilingual. German primary

### Technology
- **Display:** Large-format e-ink, 500 × 350mm. Updates once daily at midnight (counter resets and re-displays 0 → count for the day). Intermediate updates every 30 min via LoRa from corridor nodes
- **LED border:** 25mm, 3,000K warm white strip. Activates on approach
- **Sensor:** LiDAR, 6m approach zone. Pedestrian and cyclist presence triggers LED border activation
- **Power:** Mains (city centre)
- **Network:** LoRa 868MHz receiving aggregate from Type A nodes along corridor

### Response Behaviour
1. Display always visible — e-ink holds state at zero power
2. User enters 6m zone → LED border ramps from 0% to 80% over 2s
3. Border holds for 60s after last presence, then ramps down over 5s
4. Counter updated every 30 min — no individual event recorded

### Quantity on Route
- Segment 5 (Porschestrasse): 1 unit at arrival point

**Total: 1 unit**

---

## Route Deployment Summary

| Segment | Type A | Type B | Type C | Type D | Type E | Type F |
|---|---|---|---|---|---|---|
| 1 · Within Detmerode | 4 | — | — | — | 2 | — |
| 2 · Zusammenrücken Bridge | — | 2 pairs | — | — | — | — |
| 3 · Rothehofer Forst | — | — | 18 | 1 | 1 | — |
| 4 · Westhagen | 2 | — | — | — | 1 | — |
| 5 · City Centre Approach | 5 | — | — | — | — | 1 |
| **Total** | **11** | **4 pylons** | **18** | **1** | **4** | **1** |

**Total installations: 39 units** across 5 segments

---

## Shared Technical Standards

### Sensing
All active types use either IR thermal (Type A) or solid-state LiDAR (Types B, C, D, F). No camera data at any point. No microphones. No biometric sensing.

### Processing
All edge nodes run on ARM Cortex-M class microcontrollers. Detection data processed locally, result = anonymous vector or presence flag. Raw data discarded within 50ms of capture. Aggregate counters stored locally (non-volatile flash), transmitted via LoRa.

### Power
- Solar primary for remote types (A, D, and C master node): 20–30W cell, 3–5 day battery autonomy
- Mains for bridge-adjacent (B) and city centre (F) types
- All low-voltage DC internally: 12V or 24V from AC adapter or solar controller
- LED drivers: constant-current, dimmable via PWM

### Network
- LoRa 868MHz (EU868 band) for aggregate data sync between nodes
- No real-time data transmission to external systems
- No WiFi, no Bluetooth, no 4G/LTE
- All data stays within the corridor node network

### Materials Palette
| Component | Material | Rationale |
|---|---|---|
| Posts (A, B) | Weathering steel (Corten) | Low maintenance, urban-appropriate, patina over time |
| Forest post (D) | Douglas fir / Larch, FSC | Integrates with forest setting, no paint maintenance |
| Panels | 316 stainless, etched | Permanent, readable, tamper-resistant, no reprint costs |
| Ground fixtures (C) | Anodised aluminium + glass | IP68, anti-slip, minimal visual intrusion |
| Housings | Dark powder-coated aluminium | Neutral, weather-resistant |
| Fixings | 316 stainless | Corrosion-resistant in all exposed locations |

### Maintenance Schedule
- Type A: Annual inspection. Solar cell clean. SD card / firmware update via service port. E-ink panel replacement cycle: 10 years typical
- Type B: Semi-annual inspection. LED strip replacement: 50,000hr rated (>5 years continuous)
- Type C: Annual inspection. Individual fixture replacement: plug-and-replace (IP68 waterproof connector)
- Type D: Annual inspection. Timber treatment re-application: 5 years. Audio content updated as needed via USB
- Type E: No scheduled maintenance beyond annual check. LED strip: 50,000hr rated
- Type F: Annual inspection. Display module replacement: modular front-access panel

---

## Design Principles Applied

> The installation does not change the route. It changes the reality of walking it.

Each typology is calibrated to the specific cognitive task required at that point in the journey:
- At a junction: Type A gives direction without requiring a phone
- At a threshold: Type B marks the crossing as meaningful
- In an enclosed corridor: Type C makes the walker visible to themselves
- At a standstill: Type D offers the reason to stop and listen
- Alongside a building: Type E names what was always there
- At the destination: Type F acknowledges arrival publicly and anonymously

No typology requires the user to do anything. The installations respond. The walker continues.
