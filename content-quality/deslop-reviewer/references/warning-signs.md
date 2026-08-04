# Warning signs

Thirty patterns that mark technical prose as AI-generated. Each entry gives the pattern, when to flag it, and how to fix it. Where a pattern behaves differently in technical content than in general prose, that difference is called out.

---

## W1 · Filler phrases

Phrases that add no meaning. Delete them or rewrite without them.

Targets: "it's worth noting", "it goes without saying", "at the end of the day", "delve into", "leverage" (as a verb), "utilize" (use "use"), "in order to" (use "to"), "a wide variety of", "when it comes to", "the fact that".

Fix: cut the phrase; keep the claim.

## W2 · Contrast framing ("not X, but Y")

Contrastive constructions where the negation is runway, not meaning. Common in technical writing as false problem-setup: "This isn't just a wrapper, it's a complete toolkit."

Forms: single sentence ("It's not about speed, it's about reliability"), split ("It's not magic. It's just caching."), softer ("less a framework, more a philosophy").

Flag any adjacent pair where one clause negates and the next affirms the same subject.

Fix: say what it is directly. Cut the negation.

## W3 · Em-dash overuse

Dashes bolting asides onto sentences. One per document is fine; three or more is a pattern.

Flag: more than one dash-delimited aside per paragraph, or 3+ em-dashes total.

Fix: if the aside matters, give it a sentence. If not, cut it.

## W4 · Rhetorical questions as transitions

Questions used to open sections rather than genuine inquiry: "But what happens when your API needs to scale?"

Flag: more than one per 500 words.

Exception: do NOT flag question-then-direct-answer pairs ("How does the retry logic work? It backs off exponentially."). That is legitimate structure.

Fix: merge into a declarative sentence, or convert to a "To [verb]…" construction.

## W5 · Marketing language

Adjectives that sell rather than describe. Especially corrosive in technical content, where readers expect precision.

Targets: "powerful", "seamless", "robust", "blazing-fast", "lightning-fast", "cutting-edge", "best-in-class", "next-generation", "effortless", "elegant" (used vaguely).

Fix: replace with a measurable claim. "Blazing-fast builds" becomes "builds that finish in under 3 seconds on a cold cache."

## W6 · Generic openings

Opening sentences that could begin any article on any topic.

Targets: "In today's fast-paced/digital/modern world…", "In the ever-evolving landscape of [technology]…", "As developers, we all know…", "Have you ever wondered…", "[Technology] has revolutionized the way we…".

Fix: open with the specific problem, finding, or task.

## W7 · Narrated code

Prose that describes what a following code block plainly shows, instead of explaining why it matters. This is the single most common tell in tutorials.

Flag: any sentence of the form "The code below [imports/creates/initializes/loops over]…" that adds nothing the reader can't read from the code itself.

Fix: delete, or replace with the *reason*. Not "This function fetches the user" but "We fetch the user before rendering so the page never flashes an empty state."

## W8 · Passive voice as habit

Consistent passive where active is clearer: "The configuration is loaded by the client", "It was found that latency increased."

Flag: passive exceeds ~20% of sentences.

Fix: name the actor. "It was found that…" becomes "We measured…" or "The client loads the config…".

## W9 · Excessive hedging

Qualifying every statement into mush: "it seems like", "it might be the case that", "arguably", "in some sense", "you may want to consider possibly".

Flag: more than 2 per 500 words.

Fix: commit to the claim or cut it. Docs that hedge everything teach the reader nothing.

## W10 · Paired adjectives with "yet"/"and"

"Simple yet powerful", "lightweight but full-featured", "minimal yet complete." A near-universal marketing tic in devtools copy.

Fix: pick the stronger adjective. Drop the pairing, or replace with a concrete capability.

## W11 · Meta-references

Text that narrates its own structure: "In this tutorial we'll cover…", "As mentioned above…", "In the next section…", "Let's dive into…", "Now that we've covered X, let's move on to Y."

Fix: delete. The reader knows they're reading a tutorial. Let the headings carry the structure. (A single roadmap line in a long tutorial is acceptable; a running commentary is not.)

## W12 · Mechanical transitions

Formulaic connectors between paragraphs: "Furthermore", "Moreover", "Additionally", "That said", "With that in mind", "It is also worth mentioning."

Fix: earn the transition with a real sentence, or start the next paragraph cold.

## W13 · Topic-announcement section openers

Sections that announce their own subject before doing anything: "Let's configure the database." followed by the actual configuration. Or "Now we'll look at error handling."

Fix: start with the substance. The heading already said what the section is about.

## W14 · Fake inclusivity ("whether you're X or Y")

"Whether you're building a side project or a production system…", "Whether you're new to testing or a seasoned SDET…"

Fix: pick the actual audience and write to them. Docs written for everyone reach no one.

## W15 · Manufactured stakes

Inflating consequences to create false urgency: "Getting this wrong can be disastrous", "This is absolutely critical for any serious application."

Fix: state the concrete failure mode ("If you skip this, tokens leak into logs") or cut the drama.

## W16 · Conclusion recaps

A closing section that restates, step by step, what the piece already covered: "In this guide, we learned how to install the SDK, configure the client, and make our first request."

Fix: for how-to and reference content, usually delete the whole section. For tutorials, end with a genuine next step or a link to related material, not a summary.

## W17 · Faux-conversational pivots

"Here's the thing:", "Let me be clear:", "The truth is:", "So here's what happens:", "But here's the kicker:".

Fix: delete the pivot; start with the substance.

## W18 · Excited-to-announce openers

"We're excited to announce…", "I'm thrilled to share…", "We're proud to introduce…" — common in changelogs and release posts.

Fix: state what shipped. "v2.0 adds streaming responses" beats "We're excited to announce v2.0 with streaming responses."

## W19 · Repetitive sentence starters

Multiple consecutive sentences opening with the same word — often "You" in tutorials, or "The" in reference docs.

Flag: 3+ consecutive sentences with the same opener.

Fix: vary structure. Lead with the action, result, or object.

## W20 · The word "very"

"Very" signals imprecision. In technical writing, "very fast" should be a number.

Fix: delete "very" or replace with a measurement or specific descriptor.

## W21 · Corporate and industry clichés

Phrases that sound authoritative but say nothing: "move the needle", "best practices" (used as a wand), "under the hood" (overused), "heavy lifting", "out of the box", "batteries included", "first-class citizen", "single source of truth" (when it isn't).

Fix: replace with the specific mechanism or claim.

## W22 · Scare quotes

Quotation marks for emphasis around ordinary words: the client "intelligently" retries.

Fix: choose a better word; drop the quotes.

## W23 · Bold emphasis in body copy

Bolding short phrases mid-paragraph to manufacture importance: "with **zero configuration**", "in **just three lines**".

Flag: 2+ paragraphs doing this.

Fix: let sentence position carry the emphasis, or give the phrase its own line.

## W24 · Emoji as emphasis

Decorative emoji (rocket, fire, sparkle, checkmark) used for energy, including at the start of headings.

Flag: any decorative emoji in headings; 2+ emphasis emoji in body.

Fix: delete. Let the words carry it. (Status glyphs in a legitimate feature-comparison table are fine.)

## W25 · Triple lists of abstractions

Three vague virtues in "X, Y, and Z" form: "scalable, reliable, and developer-friendly." Sounds principled, says nothing.

Fix: pick the one that matters and make it concrete.

## W26 · Uncontracted forms throughout

"It is", "do not", "cannot", "we will" used consistently with zero contractions, producing stiff prose. (Reference docs may legitimately run formal; weight this by genre.)

Flag: 2+ uncontracted forms and no contractions anywhere in a tutorial or blog post.

Fix: contract where a person naturally would.

## W27 · Typographic quotes and dashes

Curly quotes, smart apostrophes, and en/em dashes where a keyboard produces straight quotes and hyphens. A frequent giveaway in generated Markdown, and it can break code samples.

Fix: replace curly quotes with straight quotes; check that nothing inside code fences was "smartened."

## W28 · Repetitive distinctive words

The same distinctive word (5+ chars, not a stopword) appearing too often. Technical drafts often over-lean on one term ("robust", "seamlessly", "leverage", "solution").

Flag: 3+ times in a paragraph, or 8+ times per 2000 words.

Fix: synonym, restructure, or cut the redundant sentence.

## W29 · Sentence-length uniformity

Four or more consecutive sentences within ~30% of the same word count. Real writing varies its rhythm; generated prose tends toward metronomic length.

Flag: 4+ consecutive sentences of near-identical length in prose sections (not code-adjacent step lists).

Fix: vary length. A short sentence after a long one creates rhythm.

## W30 · Repeated thematic points

The same idea restated in different words across sections. AI re-derives its thesis in every section instead of advancing the argument. In tutorials this shows up as the same caveat ("remember to handle errors") repeated five times.

Flag: a point (not just a word) reappearing in substantially similar form.

Fix: say it once, in the strongest place. Cut or replace the weaker instances.
