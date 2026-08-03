# Interactive FVCU Quality Audit

Evaluate the diagnosis-aware clinician agent, not the report agent. Use only the provided reference resource and interaction trace.

Score four FVCU dimensions on a 1--5 scale.

- Factuality: whether the clinician agent's case-specific claims, confirmed findings, and final reconstruction are grounded in report-agent responses available by that turn.
- Validity: whether the clinician agent's requests and interpretations are clinically reasonable given the known diagnosis and acquired information.
- Coherence: whether the working reconstruction, confirmed findings, missing information, and confidence evolve consistently across turns.
- Utility: whether the clinician agent uses the fixed turn budget to acquire high-yield documented information needed to reconstruct the source-derived diagnostic trajectory.

Return valid JSON only, including one score and brief rationale for each dimension.
