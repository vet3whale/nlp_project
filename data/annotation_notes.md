# Annotation notes

- **Stress bounds:** Preserve the stress-rating context; these limits do not guarantee normal operation.
- **Exclude:** ESD/latchup qualification ratings, unbounded thermal characteristics, typical-only values, register addresses, and descriptive thresholds. Use `requirements: []` for negatives.
- **Warnings and relationships:** Do not turn possible degradation warnings or timing relationships without stated bounds into hard limits.
- **Conditions:** Record temperature, mode, test settings, or rating context. Use `null` when none is stated; do not invent conditions or label shared test settings as separate requirements.
- **Tables:** Keep column meanings and applicable conditions. Unused cells may be omitted; check ambiguous alignment against the PDF.
- **Prose:** Normalize whitespace and retain enough context when selecting excerpts.
- **Accuracy:** Signed accuracy bounds describe measurement error.
- **Units:** `VDD` and `VDDIO` mean multiples of the reference voltage, not fixed voltages.
- **Review status:** The user checked all 220 objects against their passages. The corrections below were applied afterward and need final confirmation; passage consistency does not independently establish PDF accuracy.
- **Dataset:** 220 examples; 177 positive and 43 negative (19.5%).
- **Splits:** Preserve the pilot assignments; apply GroupShuffleSplit twice to the new families with seed 42. Training: 135 examples / 7 families. Validation: 40 / 2. Test: 45 / 3. Assignments and indices are in `data/splits/manifest.json`.
- **Test families:** BME280, FDC1004, SHT31. Keep them fixed and exclude them from model and hyperparameter selection.
- **New sources:** Official manufacturer PDFs. URLs, revisions, hashes, physical PDF pages, and one-based entry references are in `data/source_references.json`.
- **New prose:** Selected prose was shortened or paraphrased; table facts were normalized into column labels. Labels were authored by the assistant, without regex or an external labeling API.
- **Family grouping:** The SHT3x variants share one family (the selected examples use SHT31). INA219A/B and TMAG5273 variants likewise remain within their respective families.
## Combined dataset

- `data/combined.json` concatenates the twelve annotated files without changing records.
- Order is preserved, not shuffled. Use the original per-family files to construct grouped splits.
- `hdc1080.json`: entries 1-25 (one-based).
- `mpl3115a2.json`: entries 26-50 (one-based).
- `opt3001.json`: entries 51-75 (one-based).
- `tmp117.json`: entries 76-100 (one-based).

- New families are appended alphabetically: BME280 (101-115), FDC1004 (116-130), INA219 (131-145), MCP9808 (146-160), SGP30 (161-175), SHT31 (176-190), TMAG5273 (191-205), VEML7700 (206-220).

## Passage-review corrections

- **Scope:** Numerical engineering constraints only. Nonnumeric obligations (including objects 190 and 205) remain negative examples.
- **Conditions:** Include applicable ranges, timing definitions, reference levels and operational restrictions. Retain cross-references without inferring the missing figure or table content.
- **Verification status:** Design/characterization and production-testing qualifiers stay in the passage; they are not applicability conditions. Objects 123-126 and 213-217 are unchanged.
- **4-7, 22, 41-42, 44-45:** Restored operating-range qualifiers, startup communication restriction, turn-on-time definition and logic reference levels.
- **161:** The lower voltage bound explicitly also applies under maximum current demand; the upper bound remains unconditional.
- **187:** Removed the device name absent from the passage.
- **49:** Replaced the ambiguous 250 ns prose with MPL3115A2 Table 8, PDF page 10: repeated START setup time MIN 0.6 µs.
- **100:** Replaced the tentative hold-time footnote with TMP117 section 6.7, PDF page 7: data-valid time MAX 0.9 µs, retaining the timing definition from footnote 2.
- **Totals:** 220 examples, 275 requirements, 43 negatives. Object numbers are one-based in combined.json. Family assignments and split indices are unchanged.
