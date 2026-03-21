# UCP Conformance Test Suite (nan-conformance) Style Guide

<!--*
freshness: { owner: 'chadliu' reviewed: '2026-03-21' }
*-->

This guide defines the standards for the `ucp-conformance-tests`, focusing on rigorous, automated validation of UCP implementations.

## Core Principles

### 1. Brand Neutrality
*   **DO NOT** use brand names (e.g., Target, Shopify) in test cases, logs, or documentation.
*   **DO** use role-based terms: `Merchant`, `Provider`, `Agent`, `Buyer`.
*   **Test Data:** All entries in `test_data/` must be generic and brand-neutral.

### 2. Test Rigor
*   **Happy Path:** Every capability must have at least one successful "Happy Path" test.
*   **Error Handling:** Every capability must have "Negative Tests" to ensure incorrect or malicious inputs are handled gracefully with appropriate UCP error codes.
*   **Idempotency:** Specific focus on idempotency tests to ensure network retries don't cause duplicate orders or payments.

### 3. Clear Failure Messages
*   **Asserts:** Every assertion must include a descriptive message explaining what exactly failed and which part of the UCP specification it relates to.
*   **Logging:** Use `absl.logging` for consistent, timestamped test output.

## Technical Standards

### Python Code Style
*   **Linter:** Ruff (configured for **2-space indentation** in `pyproject.toml`).
*   **Docstrings:** Google Style docstrings are required for all test classes and utility functions.
*   **Dependencies:** Use `httpx` for all asynchronous HTTP calls to the implementation under test.

### Repository Specifics
*   **Integration Utils:** Centralize shared test logic (e.g., authentication, payload signing) in `integration_test_utils.py`. **Avoid duplicating** setup code across different test files.
*   **Data Models:** Use `pydantic` for validating the structure of responses from the Merchant server during tests.

## Semantic Review Focus
Gemini should prioritize:
1.  **Test Coverage:** Does this PR add tests for both success and failure scenarios?
2.  **Assertion Clarity:** Are the assertion messages helpful for debugging a failed conformance run?
3.  **Redundancy:** Check if new tests can leverage existing logic in `integration_test_utils.py`.
