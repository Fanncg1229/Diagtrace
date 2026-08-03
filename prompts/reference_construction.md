# Reference Resource Construction

Given the complete PMC case report, construct a source-grounded reference resource for an interactive diagnostic benchmark.

Extract: (1) an initial presentation that does not reveal the final diagnosis; (2) a source-ordered event bank of documented clinical findings; (3) clinical-course information derived from the event bank; and (4) article-derived diagnostic references, including the final diagnosis and diagnostic reasoning when explicitly available.

Each source event must be grounded in the report text and include provenance, source order, evidence type, diagnostic role, and figure or caption linkage when applicable. Do not infer unsupported findings, introduce external medical knowledge, or treat article order as an adjudicated clinical timeline. Mark diagnosis-revealing content for protected handling. Return valid JSON only.
