# 🧪 Angular Question Review Guidelines

Use this document as a structured prompt when auditing a HackerRank Angular question. Attach the **Problem Statement (PS) screenshot(s)** and run the checklist below against the **question** and **solution** branches.

---

## ⚠️ Core Principle (Must Read)

* The **Problem Statement (PS)** is the **single source of truth**.
* The **README is NOT authoritative** — it is only a supporting file.
* If there is any mismatch:

  * ✅ Trust the **PS**
  * ❌ Do NOT rely on README

👉 Every requirement implemented in code and tests **must be traceable back to the PS**.

---

## 🛠️ How to Use

* Provide the **Problem Statement screenshot(s)**.
* Check out:

  * `question` branch (candidate-facing scaffold)
  * `solution` branch (reference implementation)
* Work through each section and record findings.
* Flag anything marked:

  * ❌ = blocking issue
  * ⚠️ = needs improvement

---

## 1. Problem Statement Alignment

**Goal:** Ensure the PS is clear, complete, and implementation-aligned.

* **Clarity** — Are all features described without ambiguity?
* **Completeness** — Are all UI states defined?

  * Loading
  * Error
  * Empty
  * Success
* **Acceptance Criteria** — Are expected behaviours/test cases explicitly listed?
* **Constraints** — Input format, types, ranges defined?
* **Mock Data / Fixtures** — Enough detail to reason without reading code?
* **Demo Asset** — GIF/screenshot matches all behaviours?
* **No Contradictions** — PS vs solution must not conflict

👉 Ignore README mismatches unless they contradict PS-driven implementation.

**Finding:**

---

## 2. Question Branch — Starter Code Audit

### 2a. Intentional Gaps

* Are all `// TODO` or placeholders only where candidates must implement logic?
* Is each gap clearly interpretable (no ambiguity)?
* Are supporting pieces provided?

  * Services
  * Models / interfaces
  * Constants
  * HTML structure (if partially required)

---

### 2b. Syntax & Runtime Errors (Non-Stub Code)

* No TypeScript errors in non-stub code (`ng build` / `tsc`)
* No broken imports or missing modules
* All referenced selectors, components, pipes exist
* No missing test hooks (e.g., `data-testid`) used in tests
* Angular module setup is correct:

  * Declarations
  * Imports
  * Providers
* `package.json` scripts work (`start`, `test`, etc.)

---

### 2c. File & Project Structure

* Follows Angular conventions:

  * `src/app/`
  * `components/`
  * `services/`
  * `models/`
* Component structure:

  * `.ts`, `.html`, `.css` properly separated
* Naming conventions:

  * Components → PascalCase
  * Selectors → kebab-case
* No unnecessary structural complexity
* Config files intact:

  * `angular.json`
  * `tsconfig.json`
  * `karma.conf.js` / `jest.config.js`

---

### 2d. Angular Best Practices

* Components follow **single responsibility**
* Proper usage of:

  * `@Input`, `@Output`
  * Services for logic (not bloated components)
* No unnecessary third-party libraries
* Change detection strategy not overly complex
* Consistent styling approach

---

**Finding:**

---

## 3. Solution Branch Audit

* All TODOs are fully implemented
* Matches **every PS requirement**
* No debug logs / TODO leftovers
* Handles edge cases:

  * Invalid input
  * Empty states
  * Async failures
* Uses Angular patterns correctly:

  * Observables / async handling
  * Proper lifecycle hooks (`ngOnInit`, etc.)
* Code is clean and production-quality

**Finding:**

---

## 4. Test Case Quality

Evaluate `*.spec.ts` files.

### 4a. Coverage

* Happy path (end-to-end flow)
* Validation / negative cases
* Error / empty states
* State transitions
* Loading state explicitly tested
* Async handling:

  * `fakeAsync`, `tick`, or proper mocking
* Proper setup/teardown (`beforeEach`, `afterEach`)

---

### 4b. Robustness

* Tests rely on DOM/output, not internals
* Deterministic (no randomness or timing flakiness)
* Clear intent per test
* Correct query usage (`query` vs `get` patterns)
* Test selectors match exactly

---

### 4c. Test Count & Granularity

* Appropriate number of tests
* No duplication
* No overly broad tests

---

**Finding:**

---

## 5. Difficulty & Effort Calibration

### 5a. Lines of Code Delta

```bash
git diff origin/question origin/solution --stat
```

| Difficulty | Expected LOC |
| ---------- | ------------ |
| Easy       | ~10–40       |
| Medium     | ~40–100      |
| Hard       | 100+         |

---

### 5b. Conceptual Requirements

List required Angular concepts:

| Concept                         | Required? | Justified? |
| ------------------------------- | --------- | ---------- |
| Data binding (`{{}}`, `[]`)     |           |            |
| Event binding (`()`)            |           |            |
| `*ngIf` / `*ngFor`              |           |            |
| Services & Dependency Injection |           |            |
| Observables / RxJS              |           |            |
| HTTP / async handling           |           |            |
| Forms (template/reactive)       |           |            |
| Component communication         |           |            |

* Concepts must match difficulty level
* No hidden/unhinted requirements

---

### 5c. Overall Difficulty

| Dimension        | Rating | Notes |
| ---------------- | ------ | ----- |
| LOC              |        |       |
| Concepts         |        |       |
| Debugging effort |        |       |
| **Overall**      |        |       |

* Matches stated difficulty?

---

**Finding:**

---

## 6. Test Pass/Fail Verification

### 6a. Question Branch — MUST FAIL

```bash
git checkout question
npm install
npm test
```

* All tests fail
* Failures are due to missing implementation (not broken setup)

---

### 6b. Solution Branch — MUST PASS

```bash
git checkout solution
npm install
npm test
```

* All tests pass
* No skipped tests
* No hidden warnings

---

**Finding:**

---

## 7. Summary Scorecard

| Area                           | Status     | Notes |
| ------------------------------ | ---------- | ----- |
| 1. Problem Statement Alignment | ✅ / ⚠️ / ❌ |       |
| 2a. Intentional Gaps           | ✅ / ⚠️ / ❌ |       |
| 2b. Syntax & Runtime Errors    | ✅ / ⚠️ / ❌ |       |
| 2c. File & Structure           | ✅ / ⚠️ / ❌ |       |
| 2d. Angular Practices          | ✅ / ⚠️ / ❌ |       |
| 3. Solution Branch             | ✅ / ⚠️ / ❌ |       |
| 4. Test Quality                | ✅ / ⚠️ / ❌ |       |
| 5. Difficulty Calibration      | ✅ / ⚠️ / ❌ |       |
| 6. Test Verification           | ✅ / ⚠️ / ❌ |       |

---

## 🧾 Overall Verdict

* **Approved** — Ready to publish
* **Approved with minor fixes** — Non-blocking issues
* **Rejected** — Requires rework

---

## 8. Reviewer Notes

[ Add observations, edge cases, or improvement suggestions ]
