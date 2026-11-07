# 📝 Refactoring & Improvement Log: Memento Mori

This document outlines the transition from the legacy implementation to the modernized, stable version of the `mementomori` script. The primary goals were to resolve critical runtime errors, fix broken mathematical logic, and align the codebase with modern Python 3 standards.

## 🚀 Summary of Changes

### 🔴 Bug Fixes (Critical)
*   **Fixed `NoneType` Comparison Error**: Resolved a crash in `get_lifetime()` where comparing an unprovided `--lifetime` argument to an integer caused a `TypeError: '>' not supported between instances of 'NoneType' and 'int'`. Added explicit `is not None` checks.
*   **Corrected Syntax Errors**: Fixed broken Python syntax for magic variables (changed `**future**` to `__future__` and `**name**` to `__name__`).
*   **Resolved Floating-Point Precision Issues**: The original script used floating-point modulo operations (`%`) to trigger "anniversary" prints. Due to IEEE 754 precision errors, these triggers were unreliable. Replaced with robust integer-based modulo logic.

### 🛠️ Logic & Reliability Improvements
*   **Stabilized Anniversary Triggers**: Implemented clean integer intervals (yearly, 5-year, and 10-year milestones) using `agedays % interval == 0`. This ensures the "Memento Mori" reminder triggers predictably on actual anniversaries.
*   **Improved Argument Parsing**: Removed fragile manipulation of `parser._action_groups` (which is an internal implementation detail of `argparse` and prone to breaking). Replaced with standard, stable argument grouping.
*   **Input Validation**: Strengthened validation for birthdates, ensuring dates in the future or before the supported range (1900) are caught gracefully with clear error messages.

### 🧹 Code Quality & Modernization
*   **Python 3 Standardization**: 
    *   Removed redundant `__future__` imports.
    *   Implemented **f-strings** (formatted string literals) for improved readability and performance.
    *   Standardized all `print` statements to Python 3 function syntax.
*   **Dead Code Removal**: Eliminated the unused `int_range` helper function to reduce technical debt and improve maintainability.
*   **Type Safety**: Refactored the logic to ensure variables like `sex` and `lifetime` are handled safely even when omitted by the user.

### ✨ User Experience (UX) Enhancements
*   **Improved Output Formatting**: Added visual separators (`===`) and structured headers to make the terminal output easier to read at a glance.
*   **Refined Verbose Mode**: The `--verbose` flag now acts as a clean toggle for immediate detailed reporting, while the default mode provides a subtle "Memento Mori" reminder if it is not an anniversary day.
*   **Enhanced Error Messaging**: Replaced generic error prints with descriptive, actionable feedback (e.g., specifying exactly why a date was rejected).

---

## 📊 Comparison Table

| Feature | Legacy Version | Modernized Version |
| :--- | :--- | :--- |
| **Python Compatibility** | Broken/Hybrid | Python 3.6+ Optimized |
| **Anniversary Logic** | Unreliable (Float Modulo) | Reliable (Integer Modulo) |
| **Missing Args Handling** | Crashes (`NoneType`) | Graceful Defaults |
| **Code Cleanliness** | High Technical Debt | Refactored/Clean |
| **Output Style** | Raw Text | Structured/Formatted |
