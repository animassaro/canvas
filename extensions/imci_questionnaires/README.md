# IMCI Questionnaires

Canvas Questionnaire templates for the WHO IMCI Fever pathway (Integrated Management of Childhood Illness, Chart Booklet, March 2014, p. 4).

This plugin **only ships questionnaire templates** — no handlers, no applications, no custom commands. Install it alongside the `clinical_pathways` plugin to make the questionnaires available in the Pathway Builder's typeahead.

## Questionnaires shipped

| Code | Name | Role in the fever pathway |
|---|---|---|
| `IMCI_FEVER_GATE` | IMCI Fever Gate | Entry screen — exits the pathway if no fever. |
| `IMCI_FEVER_COMMON` | IMCI Fever Common Assessment | Duration, measles history, exam findings, malaria-risk context. |
| `IMCI_MALARIA_TEST` | IMCI Malaria Test Result | Captures the rapid diagnostic test result for malaria-possible arms. |
| `IMCI_MEASLES_EXAM` | IMCI Measles Examination | Sub-pathway exam when measles history is positive. |

All four questionnaires set `can_originate_in_charting: true`, so they appear in the Pathway Builder's "Continue to questionnaire" dropdown after install.

## How to use

1. `canvas install extensions/imci_questionnaires`.
2. Open the Pathway Builder (provider menu → "Pathway Builder").
3. Author **Pathway: IMCI Fever**: root = IMCI Fever Gate → branch on `Yes` to IMCI Fever Common Assessment → branch onward to IMCI Malaria Test Result and terminal classifications per the WHO chart booklet.
4. Author **Pathway: IMCI Measles Sub-pathway** separately: root = IMCI Measles Examination → three terminal branches (severe / moderate / mild).
5. Provider starts the measles sub-pathway manually on the same note when the common assessment surfaces measles history. (The `clinical_pathways` plugin v0.2 does not yet support concurrent branches on one arm.)

## Adaptations from the WHO chart booklet

- **Fever duration** is captured as a banded SING (`< 7 days` / `≥ 7 days`) rather than an integer, because Canvas's declarative questionnaire YAML doesn't support an INT response type or numeric comparison operators in `enabled_conditions`.
- **Malaria-risk catchment level** is asked as a provider question rather than driven by clinic context, because the `clinical_pathways` plugin v0.2 has no pathway-variable abstraction.

## License

MIT.
