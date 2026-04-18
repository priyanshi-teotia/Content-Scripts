# React Native Question Review Guidelines

Use this document as a structured prompt when auditing a HackerRank React Native question.
Attach the Problem Statement screenshot(s) and run the checklist below against the question and solution branches.

---

## How to Use

1. Provide the **Problem Statement screenshot(s)** alongside this prompt.
2. Check out the **question branch** (the branch handed to candidates) and the **solution branch**.
3. Work through every section below and fill in the findings.
4. Flag anything that is ❌ (fail) or ⚠️ (warning) for the question author to fix before release.

---

## 1. Problem Statement Alignment

> Goal: Verify that the written PS is clear, complete, and matches the intended implementation.

- [ ] **Clarity** — Is every feature/behaviour described unambiguously? A candidate should not need to guess.
- [ ] **Completeness** — Are all UI states (loading, error, empty, success) explicitly described?
- [ ] **Acceptance criteria** — Does the PS list each required test case (or a behaviour table) so candidates know what "done" looks like?
- [ ] **Constraints** — Are input constraints (format, length, type) clearly stated?
- [ ] **Mock data / fixtures** — Are sample IDs, expected outputs, or data shapes documented enough that a candidate can reason about them without reading source files?
- [ ] **Demo asset** — If a GIF/screenshot is attached, does it faithfully show every described behaviour?
- [ ] **No contradictions** — Cross-check: does anything in the PS conflict with the solution-branch implementation?

**Finding:**
```
[ write your notes here ]
```

---

## 2. Question Branch — Starter Code Audit

> The question branch is incomplete by design. The goal is to check that the scaffold is correct and the intentional gaps are *only* the parts the candidate must fill.

### 2a. Intentional Gaps
- [ ] Are all `// Write your code here` stubs (or equivalent placeholders) **only** in the functions/files the candidate is expected to implement?
- [ ] Is there exactly one clear way to interpret what must be filled in each stub?
- [ ] Are helper utilities (data files, constants, component shells) fully provided so the candidate is not blocked by unrelated missing code?

### 2b. Syntax & Runtime Errors (Non-Stub Code)
> Incomplete stub bodies are expected. Only flag errors in code that is **not** a stub.

- [ ] No syntax errors in any non-stub file (run `npx tsc --noEmit` or ESLint if configured).
- [ ] No broken imports or missing modules in the scaffold.
- [ ] No missing `testID` props that the test file references — every `getByTestId(...)` call in the spec must have a matching `testID` in the scaffold components.
- [ ] No typos in exported names that would cause import failures.
- [ ] `package.json` scripts (`start`, `test`, `install`) are present and correct.
- [ ] All read-only files listed in the README actually exist in the branch.

### 2c. File & Project Structure
- [ ] Folder layout follows React Native conventions (`src/`, `__tests__/`, `src/components/`, `src/utils/`).
- [ ] Component files use consistent naming (PascalCase for components, camelCase for utilities).
- [ ] Each component is in its own file; no barrel-file anti-patterns that would confuse a candidate.
- [ ] Config files (`babel.config.js`, `jest.config.json`, `tsconfig.json`, `metro.config.js`) are present and unmodified from a clean scaffold.
- [ ] `.gitignore` excludes `node_modules`, build artefacts, and platform-specific files.

### 2d. Coding Methodology
- [ ] Components follow a single responsibility principle.
- [ ] State management approach (local `useState`, `useRef`, etc.) is consistent and appropriate for the question scope.
- [ ] No unnecessary third-party libraries added beyond what the question requires.
- [ ] Styling approach (StyleSheet, NativeWind/Tailwind, etc.) is consistent across all scaffold files.

**Finding:**
```
[ write your notes here ]
```

---

## 3. Solution Branch Audit

> The solution branch represents the canonical correct implementation.

- [ ] All stub functions are fully implemented.
- [ ] Implementation matches every behaviour described in the Problem Statement.
- [ ] No `console.log`, debug statements, or leftover TODO comments in the solution.
- [ ] Edge cases called out in the PS (validation, cancellation, unmount cleanup, etc.) are handled.
- [ ] Code style is clean and production-quality (a candidate can learn from this).
- [ ] No hard-coded test-specific values (e.g., never return a mocked result only because a testID is present).

**Finding:**
```
[ write your notes here ]
```

---

## 4. Test Case Quality

> Evaluate `__tests__/App.spec.js` (or equivalent) independently.

### 4a. Coverage
- [ ] **Happy path** — at least one test exercises the full successful flow end-to-end.
- [ ] **Validation / negative path** — invalid inputs are tested (wrong format, empty, boundary lengths).
- [ ] **Error / not-found state** — what happens when a valid-format input yields no result.
- [ ] **State transitions** — going from a successful result → not-found, and vice-versa.
- [ ] **Loading state** — the transient loading indicator is explicitly asserted.
- [ ] **Async handling** — fake timers or `act(...)` are used correctly; no real network calls.
- [ ] **Cleanup** — `beforeEach`/`afterEach` reset timers and unmount cleanly between tests.

### 4b. Robustness
- [ ] Tests assert on **rendered text / testIDs**, not implementation details (state variable names, internal methods).
- [ ] Tests are deterministic — no flakiness due to real timers, random data, or order dependence.
- [ ] Each test has a single, clear intent; one failing assertion clearly indicates what is broken.
- [ ] Tests use `queryByText` / `queryByTestId` when asserting absence (not `getBy...` wrapped in `try/catch`).
- [ ] `testID` values used in the spec match exactly (case-sensitive) what is in the scaffold.

### 4c. Test Count & Granularity
- [ ] Number of tests is proportional to the complexity of the question.
- [ ] No duplicate tests covering the same scenario.
- [ ] No test is so broad that many unrelated bugs would all cause it to fail (makes debugging hard for candidates).

**Finding:**
```
[ write your notes here ]
```

---

## 5. Difficulty & Effort Calibration

### 5a. Lines of Code Delta (Question → Solution)

Run:
```bash
git diff origin/question origin/solution --stat
```

| File | Lines Added | Lines Removed |
|------|-------------|---------------|
|      |             |               |

- [ ] Total lines to write is appropriate for the stated difficulty tier:
  - **Easy**: ~10–40 lines of logic
  - **Medium**: ~40–100 lines of logic
  - **Hard**: ~100+ lines of logic

### 5b. Conceptual Requirements

List every React / React Native concept a candidate must know to solve this question:

| Concept | Required? | Justified for Difficulty? |
|---------|-----------|--------------------------|
| `useState` for controlled input | | |
| `useEffect` + cleanup | | |
| `useRef` for mutable values across renders | | |
| Async simulation with `setTimeout` / fake timers | | |
| Conditional rendering | | |
| Array `.find()` / data lookup | | |
| Regex input validation | | |
| Component decomposition | | |
| *(add others as applicable)* | | |

- [ ] The concept list matches the difficulty label (Easy questions should not require advanced patterns like context, reducers, or custom hooks).
- [ ] No concept is required that is not at least hinted at in the Problem Statement.

### 5c. Overall Difficulty Assessment

| Dimension | Rating (Easy / Medium / Hard) | Notes |
|-----------|-------------------------------|-------|
| Lines of code to write | | |
| Conceptual depth | | |
| Debugging effort (partial credit path) | | |
| **Overall verdict** | | |

- [ ] The stated difficulty label matches the overall verdict above.

**Finding:**
```
[ write your notes here ]
```

---

## 6. Test Pass/Fail Verification

> This is a hard requirement. Misconfigured test suites invalidate the entire question.

### 6a. Question Branch — All Tests Must FAIL

```bash
git checkout question
npm install
npm test
```

- [ ] Every test case fails on the question branch.
- [ ] Tests fail because the stubs are not implemented, **not** because of a test or scaffold error.
- [ ] No test is trivially passing on the question branch (e.g., an assertion like `expect(true).toBe(true)`).

### 6b. Solution Branch — All Tests Must PASS

```bash
git checkout solution
npm install
npm test
```

- [ ] Every test case passes on the solution branch.
- [ ] No skipped (`it.skip`) or focused (`it.only`) tests.
- [ ] Test run completes without warnings that mask real failures.

**Finding:**
```
[ write your notes here ]
```

---

## 7. Summary Scorecard

| Area | Status | Notes |
|------|--------|-------|
| 1. Problem Statement Alignment | ✅ / ⚠️ / ❌ | |
| 2a. Intentional Gaps | ✅ / ⚠️ / ❌ | |
| 2b. Syntax & Runtime Errors | ✅ / ⚠️ / ❌ | |
| 2c. File & Project Structure | ✅ / ⚠️ / ❌ | |
| 2d. Coding Methodology | ✅ / ⚠️ / ❌ | |
| 3. Solution Branch Audit | ✅ / ⚠️ / ❌ | |
| 4. Test Case Quality | ✅ / ⚠️ / ❌ | |
| 5. Difficulty & Effort Calibration | ✅ / ⚠️ / ❌ | |
| 6. Test Pass/Fail Verification | ✅ / ⚠️ / ❌ | |

### Overall Verdict
- [ ] **Approved** — Ready to publish.
- [ ] **Approved with minor fixes** — Issues noted above are non-blocking; fix before release.
- [ ] **Rejected** — Blocking issues found; must be revised and re-reviewed.

---

## 8. Reviewer Notes

```
[ Any additional observations, improvement suggestions, or open questions go here ]
```
