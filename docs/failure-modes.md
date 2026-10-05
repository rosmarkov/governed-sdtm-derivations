# Failure modes of AI-generated SDTM derivations

## Functional failures: plausible but wrong clinical logic

When intent was only prose, the model filled the empty space with generic domain knowledge and solved a plausible but wrong clinical problem.

| Derivation | Expected | Generated | Why |
|---|---|---|---|
| Dose dates | Earliest and latest EX dates into DM reference variables | Treatment-period engines with extra flags | The phrase "dose derivation" triggered broader clinical assumptions |
| Last contact | Maximum *DTC across source domains into RFPENDTC | Lost-to-follow-up status logic with custom structures | The domain phrase activated the wrong workflow archetype |
| SUBJID propagation | Propagate the existing SUBJID from DC to the targets | A new identifier built from site and subject components | The model inferred identifier creation instead of copy-through |

Behavior examples fixed these by showing exact input rows, target variables, edge cases and expected outputs.

## Integration failures: correct logic that still failed the framework

- wrong imports
- missing decorator or configuration
- wrong function signature and project types
- wrong return object
- approved helpers reimplemented instead of called
- missing test-harness compatibility

Behavior tells the model what to compute. Project contracts tell it how to fit.

## Taxonomy: every failure points to a missing artifact

| Observed failure | Missing artifact |
|---|---|
| Wrong logic | Behavior examples |
| Inconsistent style | Project conventions |
| Wrong imports | Dependency context |
| Wrong input structure | Metadata and schemas |
| Does not fit the system | Architecture context |
| Reinvented utilities | Capability registry |

Failures are context gaps, not hallucinations. The useful question after a failure is not "why did the model hallucinate" but "which artifact was missing".

## Most useful artifact by derivation type

| Derivation type | Main challenge | Most useful artifact |
|---|---|---|
| First and last dose | Semantic over-expansion | Concrete examples |
| Last contact | Wrong clinical archetype | Maximum-date examples |
| SUBJID propagation | Model prior: construct an identifier | Copy or join directive |
| SUPPQUAL | Metadata-driven structure | Reference schemas |
| EPOCH and TAETORD | Tie-breaking and sequencing | Edge cases plus metadata |
| SE creation | Infrastructure and SQL contracts | Approved runtime pattern |

## Where engineering knowledge hides

Requirements, specifications and code are visible to an AI model only if they are supplied. Project conventions, helper functions and dependencies, metadata, review expectations, architecture assumptions and team experience are usually hidden. LLMs only see what we make explicit.
