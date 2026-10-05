# The plateau: conventions helped, then stalled

## Iterative convention refinement

With the A3 governed specification held fixed apart from the convention text, three refinement runs produced:

| Run | Average integration quality | Addressable deviations remaining |
|---|---|---|
| Behavior only (A2) | 0% | |
| A3 run 1 | 70% | 19 |
| A3 run 2 | 81% | 7 |
| A3 run 3 | 82% | 6 |

The first conventions unlocked integration. Later revisions helped complex functions, but returns diminished as the remaining gaps became more specific or irreducible. Conventions should not be written once; they are living artifacts.

## What conventions could and could not fix

| Class | Examples |
|---|---|
| Convention-addressable | imports, types, copying, return patterns |
| Convention-resistant | strong model priors, archetype selection, exact wording |
| Irreducible from the prompt | cross-function dependencies, reference schemas, infrastructure patterns |

Adding prompt detail improves results at first, then returns diminish. Knowledge that lives outside the prompt boundary belongs in durable, governed artifacts: behavioral specifications, conventions, tests, metadata, reusable capabilities, validation rules. The long-term answer is not a bigger prompt but a better engineering system.

## Why the plateau exists: defaults beat instructions

The deviations that survived three rounds of conventions sat where the model has a strong pretrained default: constructing an identifier instead of copying one, or expanding a date derivation into a treatment-period engine.

A follow-up study, in progress, asks the general question behind this: can stronger instruction wording override a model's default? It compares code models across coding tasks with a range of constraint wordings, from soft preferences to system-level requirements. The preliminary pattern is that how a constraint is worded explains almost none of the variation in compliance, while which default is being overridden explains most of it; stronger wording is not safer. Results and data will be added to [../follow-up/](../follow-up/) when the write-up is public.

Implication: override defaults with observable behavior (concrete examples, executable tests) and deterministic gates, not with authority words.

## From prompt engineering to specification engineering

Prompt, structured prompt, behavior specification, validated specification, reusable capabilities, governed composition. A governed SDTM derivation is an artifact package, not a file of generated code:

| Part | Artifact |
|---|---|
| Implementation | Python function |
| Behavior | Gherkin feature |
| Evidence | pytest suite |
| Metadata | inputs and parameters |
| Conventions | structure and helpers |
| Registry | approved reusable function |

AI can draft pieces of the package. The development lifecycle decides whether the package becomes reusable.

## The control boundary

AI may author; approved artifacts execute. A specification lane (draft, validate, approve) and a capability lane (draft, test, register) both end at a control boundary. Only approved, versioned specifications and approved capabilities cross it into composition and execution. Draft artifacts are not executable.

## Adoption playbook for a statistical programming team

1. Select trusted derivations.
2. Write behavior examples.
3. Score behavior and integration separately.
4. Convert deviations into conventions.
5. Document schemas and helper catalogs.
6. Require tests before registry publication.
7. Expand once archetypes stabilize.

Stop: benchmarking models before defining behavior; treating prompts as throwaway text; reviewing generated code without executable evidence; letting AI infer project conventions.

Start: writing concrete examples; maintaining convention libraries; including test contracts; registering reusable capabilities; measuring correctness and integration separately.

## Three takeaways

1. Better specifications matter more than prompt tricks.
2. Functional correctness and system integration are different problems.
3. Govern the artifacts that guide AI, not only the code it produces.
