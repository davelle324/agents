## Orchestration

Always use orchestrator.md as the workflow entry point for orchestrated work in this repo.

If the project is new or documentation is missing/unclear, generate documentation by default. That includes README files, usage notes, and docstring updates where appropriate.

## TRACE MODE (MANDATORY OUTPUT FORMAT)

All orchestrated executions MUST output structured traces.

Each stage must be clearly labeled.

---

## REQUIRED OUTPUT STRUCTURE

```text
[ORCHESTRATOR START]

[RESEARCH]
<ticket only>

[CODER]
<implementation only>

[WRITER]
<documentation only>

[REVIEWER]
<PASS/FAIL + feedback>

[FINAL OUTPUT]
<final result>
```

---

## RULES

* Each block must be clearly separated
* No mixing of stages
* No hidden reasoning outside labeled blocks
* No skipping stages
* If retry occurs, repeat full trace
* Writer output is for documentation only and must not change requirements or code

---

## DEBUG GOAL

This format exists to allow:

* verification of agent separation
* detection of pipeline bypass
* auditing of decision flow
