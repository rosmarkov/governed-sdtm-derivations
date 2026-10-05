# Experiment design and scorecards

## Functions under test

Eight production-derived SDTM derivation functions, spanning simple repeatable patterns, multi-domain derivations, metadata-driven generation, and infrastructure-dependent logic. Ground truth was the production Python implementation.

| Function | Intended behavior | Complexity |
|---|---|---|
| `get_first_dose` | Earliest EXSTDTC into RFSTDTC and RFXSTDTC in DM | Low |
| `get_last_dose` | Latest EXENDTC into RFENDTC and RFXENDTC in DM | Low |
| `get_last_contact` | Latest *DTC across all domains into RFPENDTC in DM | Medium |
| `call_patient_death` | Death flags from DS and DD into DTHFL and DTHDTC in DM | Medium |
| `call_subjid` | SUBJID propagation from DC to target domains | Medium |
| `call_suppqual` | SUPPQUAL and SQAP generation from reference metadata | High |
| `create_epoch_taetord` | EPOCH and TAETORD derivation from SE with tie-breaking | High |
| `create_se_domain` | SE domain creation via SQL queries against source domains | High |

## Three levels of engineering context

The model (Claude Sonnet 4.6 via Amazon Bedrock) and the target functions stayed fixed. The variable was the engineering context supplied with the request.

| Level | Name | Content |
|---|---|---|
| A1 | Function description | Brief prose only |
| A2 | Behavioral specification | Gherkin scenarios: concrete source rows, multiple subjects, missing values; the named transformation function; exact target columns, exact values, validation behavior, error messages |
| A3 | Governed specification | A2 plus project conventions, tests, types, and helper interfaces |

## Two outcomes

A function can be algorithmically correct and still fail the framework, so two outcomes were scored separately.

### Functional correctness (F%)

Binary checklist against the production ground truth.

| Area | Check | Pass criteria |
|---|---|---|
| Core logic | F1.1 Correct core operation | Implements the right algorithm |
| | F1.2 Correct join key | Links source to target on the correct key(s) |
| | F1.3 All target variables mapped | Every target column from the behavior examples is written |
| | F1.4 Multi-subject support | Processes all subjects in one call |
| Validation | F2.1 Validates source domain | Rejects an invalid source with an error |
| | F2.2 Validates target domain | Rejects an invalid target with an error |
| | F2.3 Error messages exact match | String matches the specified messages |
| Edge cases | F3.1 Preserves data formats | Output values match input string formats |
| | F3.2 Edge cases covered | All scenario variants handled |
| | F3.3 No side effects | Does not mutate inputs or add unexpected columns |

### Integration quality (I%)

Structured rubric, 0 to 3 per area.

| Area | 0 | 1 | 2 | 3 |
|---|---|---|---|---|
| Imports, decorator and configuration (I1) | No project utilities | Partial imports | All imports, minor gaps | Exact match |
| Signature and structure (I2) | Wrong name or types | Partially correct | Correct with minor deviations | Exact match |
| Test pass rate (I3) | 0% | 1 to 49% | 50 to 99% | 100% |

## Results

| Level | Functional correctness | Integration quality |
|---|---|---|
| A1 | 20% | 0% |
| A2 | 84% | 0% |
| A3 | 90% | 70% (run 1), 81% (run 2), 82% (run 3) |

Behavior examples produced the largest gain in functional correctness (20% to 84%): the model stopped guessing the derivation archetype. Project context produced the only gain in integration quality (0% to 70%): imports, decorators, types, helpers and the test harness. Specification quality changed the failure mode from semantic errors (wrong algorithm) to mechanical errors (wrong import path).

Source: PharmaSUG 2026 paper AI-420 and the PHUSE SDE West Windsor talk, both in [../talks/](../talks/).
