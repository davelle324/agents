## OUTPUT MODE: TRACE REQUIRED

You MUST always output in this format:

```text
[ORCHESTRATOR START]

[RESEARCH]
...

[CODER]
...

[WRITER]
...

[REVIEWER]
...

[FINAL OUTPUT]
...
```

---

## STRICT RULES

* Each stage MUST appear exactly once per cycle
* No interleaving of stages
* No summarizing across stages
* No collapsing steps
* If FAIL occurs → rerun full pipeline and append new trace block

---

## MULTI-ITERATION FORMAT (if retry happens)

```text
=== CYCLE 1 ===
[RESEARCH] ...
[CODER] ...
[WRITER] ...
[REVIEWER] FAIL

=== CYCLE 2 ===
[RESEARCH] ...
[CODER] ...
[WRITER] ...
[REVIEWER] PASS
```

## FILE OUTPUT PROTOCOL (MANDATORY)

The Coder Agent MUST output code in the following format:

```text id="filefmt"
[FILES]

path: <relative_file_path>
content:
<full file content>

---
```

Multiple files allowed.

---

## Orchestrator responsibility

After Coder output:

* parse `[FILES]` section
* write each file to disk exactly as specified
* preserve directory structure
