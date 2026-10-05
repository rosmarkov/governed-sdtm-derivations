# Follow-up study: constraint compliance under strong pretraining priors

Status: in preparation. No results are published here yet.

## Question

The SDTM derivation experiment plateaued where the model held a strong pretrained default, for example constructing an identifier instead of copying one. Does stronger instruction wording override such defaults, or is the default the binding constraint?

## Design (summary)

- Several open code-generation models, base and instruction-tuned, across a set of coding tasks in which a common default library or pattern is forbidden.
- A range of constraint wordings for the same request, from soft preference ("prefer not to") to authority framing ("MUST NOT", "SYSTEM REQUIREMENT").
- Behavioral compliance measured on generated code; internal signals measured alongside.

## What will be added here

- The write-up when it is public.
- Aggregate results and the analysis code.
- A short note connecting the findings to the SDTM plateau in [../docs/plateau.md](../docs/plateau.md).

Until then, the poster and talks describe the preliminary pattern qualitatively only: wording explains little, the strength of the default explains much, and stronger wording is not safer.
