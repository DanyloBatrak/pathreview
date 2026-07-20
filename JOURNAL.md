## Week 7 — Issue selection

**Issue link:** https://github.com/ascherj/pathreview/issues/153

**Issue title:** Faithfulness checker crashes when a context chunk has text: None

**Tier:** [x] Tier 1 [ ] Tier 2 [ ] Tier 3

**Problem summary:**

The `FaithfulnessChecker().check()` method builds context string by joining the "text" field from each context chank. The issue is that when chank's "text" set to `None`, `.get("text", "")` returns `None` instead of default and crash the code with `TypeError` message by joining to `None`. This bug affects on faithfullness-checking logic in `tests/unit/test_faithfulness_checker.py` where `test_none_context_chunk_text()` method fails because `.check()` not handled this case. The successful outcome would be to make context-building step treat "text" value set to `None` in same way as empty or missing one, so that checker can score feedback correctly even if chunk's input is distorted.

**Branch name:** fix/153-faithfulness-checker-none-text

**Setup confirmation:** [x] App runs locally at localhost:5173

**Cohort ledger:** [x] Issue added to cohort ledger
