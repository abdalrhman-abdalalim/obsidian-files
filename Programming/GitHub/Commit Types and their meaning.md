### **Commit Types and Their Meaning**

- **fix:** A bug fix (corresponds to a PATCH version bump in [Semantic Versioning](https://chatgpt.com?q=Semantic%20Versioning)).
- **feat:** A new feature (corresponds to a MINOR version bump).
- **BREAKING CHANGE:** A major change that is not backward compatible (corresponds to a MAJOR version bump). This can be indicated by adding a `!` after the type, e.g., `feat!:`, or by using `BREAKING CHANGE:` in the footer.
- Other types (commonly used based on Angular conventions):
    - **build:** Changes that affect the build system or external dependencies
    - **chore:** Maintenance tasks that don’t affect production code
    - **ci:** Changes related to continuous integration
    - **docs:** Documentation updates
    - **style:** Code style updates (formatting, indentation, etc., but no functional changes)
    - **refactor:** Code restructuring that does not change functionality
    - **perf:** Performance improvements
    - **test:** Adding or modifying tests