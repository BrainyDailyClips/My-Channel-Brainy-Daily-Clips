---
name: viral-script-engineer
description: Reverse-engineers viral long-form video scripts (8+ minute YouTube videos) from source transcripts and writes new, original long-form scripts on a different topic in the same structure and speaking voice. Four modes - blending multiple sources via the 13-beat template, matching ONE source closely, an anaphora/direct-address permission-giving voice, and an action-first raw-human voice with zero preamble. Trigger on "reverse engineer," "break down the formula," "write a script in this style," "make my own version," "match the beat count," "make it in our new voice," "nothing should sound like AI," or any request to build a long-form script off example viral content, even without the word "skill" or "viral." Also covers timestamped B-roll/image-description breakdowns and template extraction. NOT for short-form content (TikTok/Reels under a few minutes) - this skill is built for 8+ minute videos only.
---

# Viral Script Engineer

Turns source **long-form (8+ minute)** video transcripts into (1) a reusable structural
template, (2) a new original long-form script in a matching voice, and (3) a timestamped
B-roll/image-description spreadsheet ready for production.

**Scope: this skill is for long-form scripts only (8+ minutes / roughly 1,200+ spoken words).**
The 13-beat structure below assumes room for a dramatized personal story, a second proof story,
and a full tactic section — that shape doesn't compress into short-form hooks or Reels-length
clips. If a source transcript or requested output is clearly short-form, tell the user this
skill isn't built for that format rather than force-fitting it into the 13 beats.

Read `references/structure-template.md` and `references/voice-checklist.md` before writing
any new script — they encode the beat structure and voice mechanics this skill is built around.
Don't skip straight to writing; the quality of the output depends on doing the analysis first.

## When the user provides source transcripts

1. **Read every transcript fully.** Don't skim — the details that make a script feel human
   (specific numbers, exact timeframes, named objects) are usually buried mid-paragraph, not
   in the obvious hook or CTA lines.

2. **Map each source against the 13-beat structure** in `references/structure-template.md`.
   Note which beats each source nails and which it skips — not every viral script hits all 13,
   and that's fine, but you want to know what's actually present before blending sources.

3. **Extract the voice separately from the structure.** For each source, log:
   - Specific filler/transition words used repeatedly (e.g. "right?", "and so", "here's the thing")
   - Self-interruption or mid-sentence restart patterns
   - How often (and where) the speaker asks the viewer a direct question
   - In-line repetition for emphasis (a phrase repeated back-to-back, not just a repeated theme)
   - Whether the delivery is choppy/fragmented (good for 15-30 sec hooks) or flowing/specific
     (better for full 3-5+ min retention)
   Do NOT default to "sound raw" as a generic instruction — write down the actual tics per
   source and match them explicitly. Generic "make it sound human" produces AI-sounding output.

4. **If a source contains a numbered list/checklist** (e.g. "5 signs," "3 mistakes"), extract
   it as its own component: note the count, and whether the order builds from
   counterintuitive→obvious, escalates in severity, or is just topical grouping. Ask the user
   which ordering logic they want if it's ambiguous, since this materially changes retention.

## When writing the new script

1. **Confirm scope with the user first if any of these are unclear** (use `ask_user_input_v0`
   rather than guessing): topic, target tone/voice (which source's voice to prioritize, or a
   blend), target length/format (single flowing story vs. numbered listicle vs. chapter-style),
   and whether to include a signs/checklist section.

2. **Fill the 13-beat template** from `references/structure-template.md`. Blend elements across
   multiple sources rather than reskinning one source's story — pull the strongest hook pattern
   from one, the checklist format from another, the emotional stakes from a third.

3. **Apply the voice checklist explicitly**, not just the concept of "raw" or "polished."
   Reread `references/voice-checklist.md` before the final pass and confirm each tic actually
   appears in the draft, at a natural frequency (not on every single line — that reads as a tic
   parody rather than a real speaking pattern).

4. **Replace every vague intensifier with a specific, checkable detail.** "For a really long
   time" → "for four days straight." "A lot of money" → "$5,000." This is the single highest-
   leverage edit for making output sound human rather than AI-written — do this pass explicitly,
   don't assume it happened automatically while drafting.

5. **If including a signs/checklist section**, order items deliberately: most counterintuitive
   or surprising first (this is what earns retention through the middle of the video), most
   widely-recognized/validating last (this closes the section on a satisfying "yeah, I knew it").

6. **Read the first 3 seconds in isolation** before finalizing. If it doesn't create genuine
   curiosity on its own, rewrite the hook — nothing else in the script matters if this fails.

7. **Save the script as a markdown file** to the outputs directory and present it. Use section
   headers matching the 13-beat numbering so it's easy to revise individual beats later.

## When the user wants a production-ready breakdown (timestamps + B-roll)

1. Split the finished script into individual sentences (not sub-clauses — sentence-level is
   the right granularity for B-roll planning).
2. Estimate timestamps using ~150 words per minute as the default spoken pace (state this
   assumption to the user; offer to adjust if they know their actual delivery speed).
3. For each line, write a one-line image/B-roll/text-overlay suggestion — mix direct-to-camera
   framing notes, B-roll shot ideas, and text-overlay callouts for any quotable/thesis lines.
4. Build this as an .xlsx file (see the xlsx skill for formatting conventions — professional
   font, wrapped text, frozen header row) with columns: Section, Timestamp, Script Line,
   Suggested Image/B-Roll Description.
5. Present the file. Note in your reply that timestamps are estimates based on average pace
   and will drift from the user's actual recorded delivery.

## Single-source exact-match mode (use when the user gives ONE source script to match closely)

Sometimes the user wants a new script that matches one specific source as closely as
structure allows — same beat count, same chapter/section progression, same devices (compare/
contrast pairs, concrete example lists, restated thesis per section) — without reusing any of
its exact wording. Use this mode when the user says things like "write it in the same style as
this script," "match the beat count," or "don't add extra beats."

1. **Read the full source once, end to end, before writing anything.** Note its actual section/
   chapter count and what happens in each one. Don't guess the structure from the hook alone —
   long-form sources often shift devices partway through (e.g. adding named-authority citations,
   compare/contrast pairs, or concrete example lists only in later sections).

2. **Match structure exactly — same number of sections, same progression, no added or removed
   beats** — unless the user explicitly asks for a shorter or extended version.

3. **Identify the source's actual rhetorical devices, not just its tone.** Common ones seen so
   far: named-authority citation, compare/contrast pairs ("imagine two people... one does X, the
   other does Y"), concrete example lists (several short, specific, nameable scenarios in a row),
   a thesis that gets restated and re-anchored at the start of each section, and explicit
   transition sentences bridging one section to the next. Reproduce the *devices*, not the source's
   specific sentences.

4. **Full reword required — no exact phrasing reuse, including partial phrases**, not just full
   sentences. Rewrite every sentence in new words while preserving its function in the structure.

5. **Stay anchored to the requested title/topic in every single sentence.** Do not let a beat
   drift into a related-but-different concept (e.g. a script titled around "fear" drifting into
   being about "confidence" generally, or "disrespect" drifting into "self-worth" generally).
   Re-check this explicitly — it's the single most common failure mode in this mode.

6. **Never attribute invented ideas or quotes to a real, named public figure**, even if the
   source does. If the source cites a real author/expert, either (a) ask the user which real,
   verifiable source they'd like cited and only use ideas that source actually published, or
   (b) replace the named citation with a generic equivalent ("researchers who study X have
   found...") that preserves the borrowed-authority function without inventing an attribution.
   This rule holds even when matching a source's style is otherwise the explicit goal.

7. **Run a self-audit before presenting the draft — do this even if the user didn't ask for it
   explicitly, since it catches the failure modes above before the user has to.** Check, in order:
   - Does every sentence stay anchored to the requested topic, with no drift into a related
     concept?
   - Does any phrase — even a partial phrase, not just a full sentence — match the source too
     closely?
   - Does the beat/section count and closing rhythm match the source exactly (no added or
     dropped beats unless requested)?
   - Is any idea attributed to a real named person without that person actually having said it?
   Fix any violation silently before presenting. Note explicitly to the user any deliberate
   deviation from exact style-matching (such as the real-person-attribution rule above), since
   that's a case where following the user's exact instruction would conflict with this
   constraint, and the deviation should be visible, not silent.

8. **For scripts long enough that a full self-audit of every line is impractical (15+ minutes),
   prioritize the audit on the hook, any quotable/thesis lines, and any list/checklist section —
   these carry the highest risk of drifting or of matching the source too closely. Narrative and
   transitional sections carry lower risk and need only a lighter pass.**

## Anaphora / direct-address mode (use when the user asks for the permission-giving "you do not
have to..." voice)

A sustained second-person, repeated-sentence-opener style with no third-party examples — see
`references/anaphora-style.md` for the full breakdown before writing. Use this mode when the
user references "the anaphora voice," "the permission voice," or describes a script built on
repeated openers like "You do not have to..." / "You are allowed to...".

Key mechanics to apply (full detail in the reference file): permission-giving tone rather than
accusatory; stay in direct address throughout with no named third-party proof stories; build
anaphora runs of 3+ sentences sharing an opener; close each chapter with a 3-part parallel triad;
pace in ~300-500 word chapters. **Before presenting a full draft, state the word count and
estimated runtime at both 130 and 150 wpm** — this style is often requested at 30-45+ minutes
and the length needs to be confirmed, not assumed. For long targets, it's fine to deliver a
sample chapter first, confirm direction, then build the rest. Run the style-specific audit
additions in the reference file (new idea per chapter, not padding; tone drift from
permission-giving into accusatory) alongside the standard audit above.

## Action-first / raw-human voice mode (use when the user says "our new voice," "nothing should
sound like AI," or asks for scripts that get right to it with no preamble)

Reverse-engineered from real transcripts, not a generic "sound more human" instruction — see
`references/action-first-voice.md` for the full breakdown before writing. Use this mode when
the user references "action first," wants to beat the early retention cliff, or explicitly asks
you to "make it in our new voice" after sharing example transcripts in this style.

Key mechanics to apply (full detail in the reference file): zero preamble — content starts in
the first 1-2 sentences, no topic announcement; numbered points delivered conversationally with
self-aware pacing comments; high-frequency rhetorical questions aimed at the viewer; real-only
citations (scripture, documented events, named real things — never a fabricated quote or a vague
invented "studies show" claim); raw self-interruption and informal grammar used naturally, not on
a fixed schedule; one of two structural devices per point (state→complicate→reveal-mechanism, or
mirrored-perspective "you call it X, a [strategist/psychologist] calls it Y"); announced
repetition and closing triads for emphasis; escalating stakes across points; and no stall
sentences that exist only to transition. Run the style-specific audit additions in the reference
file (preamble check, citation-reality check, stall check, rhetorical-question density) alongside
the standard audit above.

## Quick reference: the 13 beats

1. Contradiction hook · 2. Brief authority + vulnerability · 3. Promise stack ·
4. Debunk the common wrong answer · 5. Core thesis (quotable) · 6. Dramatized personal story ·
7. Universalizing principle · 8. Second proof story (different domain) ·
8.5. Optional: ranked signs/checklist · 9. Concrete small-step tactic ·
10. Preempt the objection · 11. Second thesis/twist (quotable) ·
12. Physical proof + metaphor · 13. CTA loop

See `references/structure-template.md` for the full fill-in-the-blank version of each beat.
