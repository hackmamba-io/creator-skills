# Consolidated Technical Writing Style Rules

This reference synthesizes rules from four widely adopted standards: the Google Developer Documentation Style Guide, the Microsoft Writing Style Guide, the Chicago Manual of Style, and the Apple Style Guide. Where guides agree, the rule is presented as definitive. Where they differ, the version with the strongest reader impact wins.

This is not a summary. It is a working reference for evaluating real drafts.

---

## Table of Contents
1. Voice and Tone
2. Grammar and Sentence Structure
3. Word Choice
4. Punctuation
5. Headings and Structure
6. Lists
7. Code and Technical Elements
8. Inclusive and Global Language
9. Links and References
10. Common Violations Cheat Sheet

---

## 1. Voice and Tone

**Use second person.** Address the reader as "you."
- Wrong: "The user should click the button."
- Right: "Click the button."

**Use active voice.** The subject performs the action.
- Wrong: "The file is saved by the system."
- Right: "The system saves the file."
- Exception: passive voice is acceptable when the actor is unknown or irrelevant to the reader.

**Use present tense.** Avoid future tense for describing actions and system behavior.
- Wrong: "The command will return an error."
- Right: "The command returns an error."

**Be conversational but not casual.** Write like you are explaining something to a smart colleague who has time for substance but not for performance.
- Contractions are acceptable (you're, it's, don't). Google and Microsoft both permit them.
- Avoid slang, idioms, and culturally specific expressions.

**Cut hollow affirmations.** They waste the reader's time.
- Wrong: "Great question!" / "Absolutely!" / "Certainly!"
- Right: Just answer.

---

## 2. Grammar and Sentence Structure

**Keep sentences short.** Aim for 15 to 20 words per sentence. Long sentences bury the action and make readers work for information that should be immediate.

**One idea per sentence.** If you are using "and" to connect two independent clauses, consider splitting them into two sentences.

**Use imperative mood for instructions.**
- Wrong: "You should navigate to the settings page."
- Right: "Navigate to the settings page."

**Use parallel structure in lists and headings.**
- Wrong: "Configure the server, testing the endpoint, and deployment."
- Right: "Configure the server, test the endpoint, and deploy."

**Avoid noun stacking.** Chains of nouns before a main noun are hard to parse.
- Wrong: "user authentication token validation service"
- Right: "service that validates user authentication tokens"

**Avoid nominalizations.** Use verbs, not their noun forms.
- Wrong: "Perform an installation of the package."
- Right: "Install the package."

---

## 3. Word Choice

**Prefer simple words.**

| Avoid | Use instead |
|-------|------------|
| utilize | use |
| leverage | use, build on |
| facilitate | help, enable |
| implement | add, build, set up |
| terminate | end, stop |
| commence | start |
| in order to | to |
| due to the fact that | because |
| prior to | before |
| subsequent to | after |

**Be precise with technical terms.** Define on first use if the audience may not know them. Do not define terms the audience clearly knows. That is condescending.

**Cut filler and hedge words.**
- Filler: "basically," "essentially," "simply," "just," "very," "quite"
- Overused hedges: "might," "could," "perhaps," "in some cases"

**Never use "easy," "simple," or "straightforward."** What feels simple to the writer may frustrate the reader. These words are exclusionary.

**Spell out acronyms on first use.** Format: Full Term (FT). Exception: acronyms that are more recognizable than the full form, such as API, HTML, and URL.

---

## 4. Punctuation

**Use the Oxford comma.** All four major guides recommend it for technical writing.
- Wrong: "Configure the server, test the endpoint and deploy."
- Right: "Configure the server, test the endpoint, and deploy."

**Use sentence case for headings, not title case.** Google and Microsoft both recommend this.
- Wrong: "How to Configure Your API Key"
- Right: "How to configure your API key"
- Exception: proper nouns keep their capitalization.

**Avoid exclamation marks.** One per document is the absolute maximum. They read as performative in technical content.

**Do not use ampersands in prose.** Spell out "and."

**Periods go inside quotation marks** when following US English conventions, which most technical style guides use.

---

## 5. Headings and Structure

**Headings should describe content, not just label it.**
- Wrong: "Overview" (too vague)
- Right: "How the authentication flow works"

**Task-based headings use either gerunds or infinitives, consistently.**
- Gerund style: "Installing the package," "Configuring the server"
- Infinitive style: "Install the package," "Configure the server"
- Pick one pattern and use it throughout the document.

**Do not skip heading levels.** Move from H1 to H2 to H3 only. Never from H1 to H3.

**Front-load the most important word.** Readers scan headings. Put the keyword first.
- Wrong: "A guide to setting up authentication"
- Right: "Authentication setup guide"

---

## 6. Lists

**Use bulleted lists for unordered items. Use numbered lists for sequential steps.**
- Do not use numbered lists for non-sequential items just because there are several of them.

**All list items must be parallel.** Same grammatical form throughout.

**Lead list items with the key term.** Readers scan lists.
- Wrong: "You can use this method to authenticate users."
- Right: "Authentication: use this method to verify user identity."

**Introduce every list with a stem sentence ending in a colon.**
- Wrong: [List with no introduction]
- Right: "The package includes three components:"

**Keep list items concise.** If a list item needs more than two sentences, it is a section, not a bullet.

**Minimum two items per list.** A single-item list is a sentence.

---

## 7. Code and Technical Elements

**Use code font for all inline code, commands, file names, paths, and values.**
- Right: "Run `npm install` to install dependencies."
- Right: "Open the `config.yaml` file."

**Code blocks should be complete and runnable** where possible. Partial snippets that cannot be tested frustrate developers.

**Label every code block with its language.** This enables syntax highlighting and tells the reader what they are looking at.

**Never use screenshots to show code.** Code must be copyable.

**Explain what the code does before or after showing it.** Do not drop a block with no context. Do not repeat the explanation both before and after unless the code is complex enough to justify it.

**Placeholders in code use angle brackets and SCREAMING_SNAKE_CASE:**
- Right: `curl -H "Authorization: Bearer <YOUR_API_KEY>"`

---

## 8. Inclusive and Global Language

**Use gender-neutral language.**
- Wrong: "he or she," "his/her"
- Right: "they," "their" (singular they is accepted by all four major guides)

**Avoid ableist language.**
- Wrong: "sanity check," "blind spot," "crippled by," "dumb down"
- Right: "validation check," "gap," "limited by," "simplify"

**Avoid culturally specific idioms.**
- Wrong: "hit a home run," "boiling the ocean," "herding cats"
- Right: describe the concept directly

**Do not assume a US-centric context.** Avoid references to US-specific laws, systems, or holidays as universal.

**Use unambiguous date formats.**
- Wrong: "03/04/25" (is this March 4 or April 3?)
- Right: "March 4, 2025" or ISO 8601: "2025-03-04"

**Avoid directional language for UI navigation.**
- Wrong: "Click the button on the left."
- Right: "Click Settings." (Interfaces change. Directions become wrong.)

---

## 9. Links and References

**Use descriptive link text.** Never use "click here" or "read more."
- Wrong: "For more information, click here."
- Right: "See the authentication guide for details."

**Link text should make sense out of context.** Screen readers read links in isolation.

**Do not link to the same destination multiple times in close proximity.** Once per section is enough.

---

## 10. Common Violations Cheat Sheet

| Violation | Why it matters | Fix |
|-----------|---------------|-----|
| Passive voice | Obscures who does what | Identify the actor; rewrite as subject-verb-object |
| Future tense | Creates distance from the action | Switch to present tense |
| "Simply" / "easily" | Alienates readers who struggle | Delete the word |
| Noun stacking | Hard to parse | Rewrite with prepositions |
| Missing Oxford comma | Creates ambiguity | Add comma before the last "and" |
| Title case headings | Inconsistent with developer docs standard | Convert to sentence case |
| Hollow affirmations | Wastes reader time | Delete entirely |
| Undefined acronym | Excludes readers | Spell out on first use |
| "Click here" links | Inaccessible out of context | Use descriptive anchor text |
| No code labels | Reader cannot tell the language | Add language tag to code block |
| Nominalizations | Makes writing heavy | Use the verb form |
| Culturally specific idioms | Fails global audiences | Replace with direct description |
