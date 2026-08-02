Chaldea.moe — Concept Doc

Premise: chaldea.moe is not a portfolio, it's a hub. Each project/site you've built is a "place" on a Chaldea-style map, gated by a character who thematically fits that project. Visiting is a navigation + dialogue experience, not a page load.

Entry flow:

Land on chaldea.moe → Mash greets you (short intro dialogue, orientation only, no gating).
Mash gestures to a marker/panel in the corner → click it → map opens.
Map shows markers, one per project/place. Style: fits Chaldea aesthetic (dark background, facility/constellation feel — TBD exact visual).

Per-marker flow:
4. Click a marker → resident character for that project opens a dialogue box.
5. Character explains the project in-personality, one line at a time. Skippable.
6. If not skipped, dialogue ends with a prompt: "interested?" → two choices, Yes / something else.
7. Yes → link/handoff to the actual project subdomain (e.g. BB.chaldea.moe), where the site's whole visual/interaction theme matches that character. On the subdomain, character greets you again and walks you through how it's implemented (technical depth lives here, not on the hub).
8. No → character-specific reaction, then kicked back out to the map (or back to Mash, per character).

Character-to-project mapping (thematic, not arbitrary):

Mash → hub navigator only, no project, no gate.
BB → BB project. Has a reject-loop mechanic: since BB canonically controls time, rejecting her sends you back to a re-asked version of the same choice — diegetic, not just a UI gimmick. Capped at 3 escalating rejection variants, then cycles/repeats.
Ritsuka → masterrecord (portfolio site). Fits since "Master Record" = the Master's record. Straight walkthrough, no reject-loop (doesn't fit the master/servant framing).
Future characters → mechanic per marker should be derived from that character's actual kit/personality, same way BB's loop comes from her time control. Not every marker needs a special mechanic — only add one if it's actually justified by the character.

Content split:

chaldea.moe (hub): natural-language explanation of what the project does and why.
project subdomain: technical walkthrough of how it's implemented, narrated in-character.

State/persistence:

localStorage only, no backend.
Tracks: mash_intro_seen, per-project rejections count, per-project visited flag.
Returning visitors: skip Mash's intro if already seen, drop straight to map (Mash intro should itself be skippable).

Tech:

Vue + TS + Vite, no flakes, plain shell.nix if needed for tooling.
Shared dialogue engine: takes a script object ({ speaker, line, expression, choices? }[]), one DialogueBox.vue + a useDialogue(script) composable that also owns the localStorage read/write.
Rejection-loop / choice-consequence logic lives outside the dialogue data itself (in the composable/handler), so it's reusable across any future character who gets a similar gate — writing a new marker becomes "new script + new sprite sheet," not new engine code.
Sprites: FGO assets for personal fan-use version; AI-generated/original fallback kept in reserve for any context where using ripped IP art would be a liability.

Explicitly not:

Not a hiring-portfolio funnel (masterrecord already serves that role separately). This is pure vibes/navigation/date-experience — BB can be as unhinged as she actually is, no professional-safety pressure on tone.

Build order (agreed sequencing):

Prove the concept end-to-end with BB only: full dialogue set (4–5 beats: what/why/design decision/technical detail/link-out) + reject-loop + handoff to BB.chaldea.moe.
Once that feels right in-hand, generalize the engine and add Mash + Ritsuka/masterrecord.
Expand marker by marker after that, choosing each new character's mechanic from their canon powers/personality.

