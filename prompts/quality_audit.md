# Reference Resource Quality Audit

Evaluate benchmark data quality, not downstream model performance. Use only the supplied source report text and extracted reference resource. Do not add external medical facts.

Identify a compact inventory of major diagnosis-relevant findings from the source report. For each source finding, decide whether it is represented in the source-ordered event bank. For each extracted event, decide whether it is faithful to its supporting source quotation. For each article-derived diagnostic reasoning item, decide whether it is supported by the source-ordered event bank and diagnostic references. Return valid JSON only.
