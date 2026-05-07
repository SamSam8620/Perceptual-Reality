# Mixed Reality — Wolfsburg Active Corridors

## Concept
A daily car user finds a 20-minute walk exhausting; a daily walker covers the same distance with ease. The same physical route carries two entirely different realities depending on the person experiencing it. This project asks: **what if every user had a fixed but personally calibrated reality for that walk — without carrying any device to make it happen?**

This is a network of device-free, privacy-safe ambient installations embedded into existing pedestrian and cycling routes across Wolfsburg, enriching the experience of moving toward the city center (Porschestrasse) from all surrounding districts.

---

## Context: Wolfsburg, Germany
Wolfsburg is a car-centric city by design — purpose-built in 1938 around the Volkswagen factory. Its urban density is disproportionate: Porschestrasse and the city center are walkable and activated, but surrounding residential districts (Westhagen, Detmerode, Laagberg, Klieversberg, Nordsteimke, and others) are loosely stitched together by weak, underused, or uninviting pedestrian and cycling corridors.

The car dominates not just the infrastructure but the *culture* of movement. Active travel feels effortful and unrewarding. The problem is not only physical — it is perceptual.

---

## Problem
- Surrounding districts are poorly connected to Porschestrasse for non-car users
- Routes exist but feel long, unsafe, or characterless — reinforcing car dependency
- Perceived distance is greater than actual distance for habitual car users
- No system currently bridges the gap between the physical route and the user's experience of it

---

## Proposed Solution: Ambient Route Infrastructure
A network of **device-free, sensor-driven installations** placed at key nodes and along route corridors that:

### Detect — without identifying
- Presence and movement detected via **LiDAR, infrared thermal sensors, or radar**
- No cameras, no facial recognition, no personal data captured
- System responds in real-time and immediately discards raw data — no logs, no profiles
- Only **anonymous aggregate signals** are used (e.g. flow count, direction, pace estimate)

### Respond — in real-time
Installations react to pedestrian and cyclist presence, making the route feel alive and inhabited:
- Dynamic lighting that activates ahead of the user's path
- Directional audio cues at decision points (junctions, underpasses, open spaces)
- Visual projections or surface-embedded displays triggered by movement

### Enrich — the experience of the route
Three layered content types:

**1. Wayfinding**
- Distance and time-to-center shown contextually at key nodes — not on a screen the user carries, but embedded in the environment
- Progress markers that reframe distance as achievable segments
- Subtle directional cues at confusing or disconnected junctions

**2. Cultural & Historical Overlays**
- Projections and installations referencing Wolfsburg's unique history: the factory city, VW, the canal, the Allerpark, the modernist planning era
- Each district's route carries the character of that neighborhood
- Makes the walk feel like a journey through the city's identity, not just a commute

**3. Social Cues**
- Aggregate counters: "482 people walked this route today" — motivating without identifying
- Visual density indicators showing where pedestrian activity is highest
- A sense of shared presence without surveillance

---

## Key Design Principle
> The route doesn't change. The infrastructure makes the reality of walking it different.
> No device required. No data kept. Every user has a distinct but shared experience.

---

## Design Output
A **site-specific urban design proposal for Wolfsburg** comprising:
- Mapping of weak pedestrian/cycle links between all major districts and Porschestrasse
- A typology of installation interventions matched to route conditions (underpass, open boulevard, park edge, junction, etc.)
- Node-by-node placement strategy across the active corridor network
- Technical specification for sensing and response systems
- Experience storyboards: the walk from each district, before and after intervention
- Implementation phasing and material recommendations

**Goal:** A deployable design that measurably increases pedestrian and cycling traffic by reducing perceived effort and enriching route experience.

---

## Districts in Scope
| District | Route Character | Key Challenges | Status |
|---|---|---|---|
| **Detmerode** | Modernist Großsiedlung → forest corridor → Westhagen → center | Poor legibility, perceived length, weak entry/exit nodes | **Pilot — analysis complete** |
| Westhagen | Long straight corridors, active renewal zone | Monotony, through-zone legibility | Pending |
| Laagberg | Park-adjacent | Underused green routes | Pending |
| Klieversberg | Elevated, residential | Gradient, disconnection | Pending |
| Nordsteimke | Northern fringe | Distance, low footfall | Pending |
| _Others TBC_ | | | |

### Detmerode Pilot — Route Summary
**Detmerode → Porschestrasse:** ~3.5–4 km | ~45–55 min walk | ~15–20 min cycle

Five segments identified, each with distinct character and intervention type:
1. **Within Detmerode** — estate legibility, wayfinding nodes
2. **Zusammenrücken Bridge** (2021, 90m, crosses Braunschweiger Str.) — journey gateway moment
3. **Rothehofer Forst** — landscape corridor, responsive lighting + audio
4. **Westhagen transition** — directional reinforcement through renewal zone
5. **City center approach** — intensifying social cues, arrival signal at Porschestrasse

**Cultural anchors on this route:** Alvar Aalto's Stephanuskirche (1968), "Don Camillo" & "Peppone" towers, Mittellandkanal, Rothehofer Forst planned buffer landscape.

Full analysis: [`/research/detmerode_analysis.md`](research/detmerode_analysis.md)
User journey storyboard: [`/storyboards/detmerode_user_journey.md`](storyboards/detmerode_user_journey.md)

---

## Technology Stack (Installation-Level)
| Function | Technology | Privacy Rationale |
|---|---|---|
| Presence detection | LiDAR / Infrared thermal | No image capture, no identity |
| Movement tracking | Radar / ultrasonic | Anonymous vector, discarded live |
| Response layer | Embedded LED, projection, directional audio | Output only, no input stored |
| Aggregate data | Edge-processed counters | Never leaves the node |

---

## Research Questions
- Which route segments are the weakest links between each district and Porschestrasse?
- What is the perceived vs. actual distance gap for car-habitual users in Wolfsburg?
- Which installation typologies most effectively reduce perceived effort?
- How does cultural specificity in overlays affect route adoption?

---

## Status
> Pilot district (Detmerode) — route analysis + user journey storyboard complete — 2026-04-30
> Next: Installation typology design — what the physical objects look like and how they behave

---

## Project Structure
```
/research
    detmerode_analysis.md          ✓ complete
    [district].md                  — pending for remaining districts
/design
    — installation typologies      pending
/storyboards
    detmerode_user_journey.md      ✓ complete
    [district]_user_journey.md     — pending for remaining districts
/technical
    — sensor specs, system diagrams  pending
```

---

## License
_To be determined._
