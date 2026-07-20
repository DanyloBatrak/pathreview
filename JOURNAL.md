## Week 7 — Issue selection

**Issue link:** https://github.com/ascherj/pathreview/issues/153

**Issue title:** Faithfulness checker crashes when a context chunk has text: None

**Tier:** [x] Tier 1 [ ] Tier 2 [ ] Tier 3

**Problem summary:**

The `FaithfulnessChecker().check()` method builds context string by joining the "text" field from each context chank. The issue is that when chank's "text" set to `None`, `.get("text", "")` returns `None` instead of default and crash the code with `TypeError` message by joining to `None`. This bug affects on faithfullness-checking logic in `tests/unit/test_faithfulness_checker.py` where `test_none_context_chunk_text()` method fails because `.check()` not handled this case. The successful outcome would be to make context-building step treat "text" value set to `None` in same way as empty or missing one, so that checker can score feedback correctly even if chunk's input is distorted.

**Selection notes ("Is this right for me?" checklist):**

- **Understanding:** I can descrive this issue in such way: `check()` builds a context string from chunk using `chunk.get("text", "")`, but this only defaults when the key is "missing". If "text" is present and would be set to `None` then `.get()` returns `None`, and the later `" ".join(...)` call would crash the code with `TypeError` message.
- **Affected area:** The issue is in `FaithfulnessChecker.check()`. The failing test `test_none_context_chunk_text` in `tests/unit/test_faithfulness_checker.py` confirms it.
- **Definition of done:** Before the fix: passing a chunk like `{"text": None}` crashes with a `TypeError` message. After the fix: `check()` should treat that chunk's text as empty or missing one and still return a correct score feedback. 
- **Tier fit:** This is a Tier 1 issue because it requires one or two line fix that isolated to a single method, fully covered by an existing test and with no cross-module dependencies. This is my first contribution to a large codebase, which is why Tier 1 would be my starting point.
- **Codebase readiness:** I've located `check()` through `tests/unit/test_faithfulness_checker.py` and the surrounding context-building logic, and read `test_none_context_chunk_text` from start to finish in the test file.
- **Scope/time:** Based on the issue, I estimate 3-6 hours (Tier 1 estimate for Week 8-9) since it looks look like a 1-2 line fix with verifying the existing test passes. 
- **Blockers:** No open blockers or dependencies are noted in the issue.

**Branch name:** fix/153-faithfulness-checker-none-text

**Setup confirmation:** [x] App runs locally at localhost:5173

**Cohort ledger:** [x] Issue added to cohort ledger
