# Word Quest Vocabulary

The canonical corpus is `data/sets/` plus `data/vocabulary-manifest.json`.
The website embeds the generated corpus; rebuild it after changing source data.

| Editorial study level | Words | Lessons |
|---|---:|---:|
| SSAT Elementary (current grades 3-4) | 111 | 6 |
| SSAT Middle (current grades 5-7) | 273 | 14 |
| SSAT Upper (current grades 8-11) | 224 | 12 |
| Total | 608 | 32 |

All three SSAT levels combine Carryword with WordNet-curated sets. The 130
former advanced-academic words were individually reclassified: 65 to Middle
and 65 to Upper. These are
independent study recommendations, not official SSAT vocabulary lists,
source-provided age ratings, a calibrated difficulty scale, or a complete
exam-preparation curriculum. Grade bands follow the
[assessment provider's SSAT levels](https://www.admission.org/assessments/ssat/about-the-ssat).
Learners may review earlier levels; a word's study level is separate from
the learner's scored mastery.

Placement considers concreteness, familiarity, abstraction and reasoning:
Elementary emphasizes everyday language and accessible descriptive words;
Middle emphasizes academic verbs, context and contrasts;
Upper emphasizes abstract concepts, nuanced traits and less familiar terms.
This is editorial judgment, not a measured grade rating. Some
words intentionally appear below the level at which a learner might first
encounter them. Levels are individual scopes, not cumulative pools; use
All levels to review across levels.

The Exam filter selects overlapping editorial level bands:

| Exam | Included levels | Words |
|---|---|---:|
| SSAT Elementary | Elementary | 111 |
| SSAT Middle; ISEE Lower | Elementary, Middle | 384 |
| SSAT Upper; ISEE Middle | Elementary, Middle, Upper | 608 |
| PSAT 8/9; ISEE Upper; PSAT/NMSQT; SAT; ACT | Middle, Upper | 497 |

SSAT grades refer to current grade and ISEE to the grade being applied to.
These broad pools are recommendations, not individual word-level exam
classifications or evidence of exam coverage. Exam, Level, Lesson and
Mastery filters intersect. Progress is shared.

Lessons contain 15-20 words, with light themes and an editorial
sequence from foundations toward reasoning and mixed review. They are not
alphabetical slices or official SSAT lessons. Related terms are deliberately
compared in some lessons, but each includes varied meanings and tasks.
`data/lessons.json` is the canonical registry of permanent lesson IDs and
explicit word-ID memberships. All lessons supports mixed review; mastery
can further filter any lesson.

Future expansion appends new words to existing lessons or adds new lesson
IDs. It does not regenerate IDs or rebalance published memberships.
Lesson totals are derived from per-word progress, so new vocabulary starts
untested without erasing earlier mastery.

## Sources and adaptations

- 270 words from carryword's
  [English Learner Synonym Thesaurus](https://github.com/carryword/english-vocabulary/tree/91741957c8d23eb0feb7365678721b6d34cc7c65),
  under [MIT](licenses/carryword-MIT.txt).
- 338 newly authored study records selected from public headwords in
  [Open English WordNet](https://github.com/globalwordnet/english-wordnet/tree/9b6aca775ae10ad3d2dc9956e8ad42a4ce1e076b).
  Credit: The Open English WordNet Team and Princeton University WordNet.
  See [CC BY 4.0 and attribution](licenses/wordnet-LICENSE.md) and the
  [underlying Princeton notice](licenses/Princeton-WordNet.txt).

WordNet records include a reviewed `sourceSynset` for the intended sense.
Definitions, examples, clues/contrasts and levels
were newly written or selected for Word Quest. The modern figurative senses
of **abysmal** and **epiphany** are explicitly marked with `sourceSenseNote`:
their headwords occur in the source, but those study senses are original
editorial definitions, not definitions supplied by the pinned WordNet.
Licensed adaptations remain available under their source terms; the
proprietary project license does not restrict those grants.

All words are treated equally within their level, regardless of source.
The former vocab/expanded split and quiz weighting have been removed.
Schema version 2 contains no `core` classification or split counts.
Level, Lesson and Mastery are the global filters.

All study fields were reviewed for the chosen sense and example.
Examples emphasize the exact headword in Learn, Flashcards and deep dive.
The current schema has one selected sense and one synonym/clue per word.
An absent antonym entry is not necessarily a defect: many senses have no
direct opposite, and unreviewed contrasts must not be invented. Additional
synonyms and usages need sense-specific editorial review rather than
combining a word's dictionary senses into a single quiz record.
Each record has three reviewed, conservative `distractors`; quizzes do not
randomly use a near-synonym as a wrong answer. Context and opposite questions
identify the intended sense, and usage questions ask for a sentence's
meaning rather than inventing potentially valid "wrong" sentences.
These conservative alternatives favor answer clarity over close-choice
difficulty. More demanding distractors require separate editorial review.
Sixty-three words (25 existing Upper and 38 formerly academic, now assigned
to Middle or Upper) also have original,
reviewed context-inference questions. SAT/PSAT/ACT sessions favor meaning
in context; when selected words have reviewed inference questions, standard,
Challenge and God Mode use progressively more of them, targeting 15%, 30%
and 45% of the session respectively (rounded up and limited by availability).
ISEE focuses on synonyms and sentence
completion, and harder SSAT Middle/Upper sessions include analogies. This
is vocabulary practice, not a full test simulation. Practice does not create
mastery evidence.

## Dogfood replacement and coverage

This is a curated migration, not a claim that the old selection was an
independently published public list. Continuity with existing study words
informed selection alongside broader learner vocabulary. Old definitions,
examples, weekly ordering and class-derived target flags were not reused.
The former class-derived sets, inventory and embedded snapshot were removed
from the current tree in one coordinated swap.

`data/replacement-coverage.json` records **326/406 normalized spellings
(80.3%) and 63/63 former core spellings (100%)** in ready-to-quiz records.
This exceeds the issue gates of 325 and 51. Counts are spelling coverage,
not proof of identical senses, official exam coverage, or legal clearance.
The replacement includes 102 headwords beyond that baseline.

To reproduce the comparison without retaining the removed inventory:

```sh
node scripts/check-replacement.cjs
```

The check reads the pinned baseline commit locally with `git show`,
normalizes using `trim().toLowerCase()`, checks an inventory hash, and
compares canonical replacement records by exact spelling. It does not copy
the old definitions or republish a baseline inventory. The migration's
fixed ID range keeps this historical measurement reproducible when
subsequent releases add new words.

Dogfood state continuity is not a release requirement for this migration.
Replacement records receive new IDs above the existing public-source range,
and the renamed app uses a fresh browser-storage namespace. Old dogfood
progress is not imported. After external publication, updates should be
additive and must preserve learner progress.

Removing current files does **not** erase Git history, PR diffs, forks or
previously published copies. No history rewrite or force-push is part of
this migration. Review those separately before commercial distribution;
public-source licenses do not grant rights to past class-derived material.
