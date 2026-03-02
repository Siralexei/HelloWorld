# CLAUDE.md — AI Assistant Guide for HelloWorld

This file provides guidance for AI assistants (e.g., Claude Code) working in this repository.

---

## Repository Overview

**HelloWorld** is a minimal Maven-based Java project used as a test/learning repository. It contains a classic "Hello World" application and a basic JUnit test suite. Commit messages and documentation are primarily in Spanish.

- **Owner:** Siralexei
- **Remote:** `http://local_proxy@127.0.0.1:42190/git/Siralexei/HelloWorld`

---

## Project Structure

```
HelloWorld/
├── CLAUDE.md              # This file
├── README.md              # Project description (Spanish)
├── test.txt               # Sample plain-text file
└── test111/               # Maven Java sub-project
    ├── pom.xml            # Maven build descriptor
    └── src/
        ├── main/
        │   └── java/org/alexi/javabrains/test/
        │       └── App.java        # Main application entry point
        └── test/
            └── java/org/alexi/javabrains/test/
                └── AppTest.java    # JUnit 3 unit tests
```

---

## Technology Stack

| Concern          | Tool / Version         |
|------------------|------------------------|
| Language         | Java                   |
| Build system     | Maven (POM 4.0.0)      |
| Testing          | JUnit 3.8.1 (legacy)   |
| Source encoding  | UTF-8                  |
| Packaging        | JAR                    |

---

## Build & Development Workflow

All Maven commands must be run from inside the `test111/` sub-directory (where `pom.xml` lives).

```bash
cd test111

# Compile source code
mvn compile

# Run unit tests
mvn test

# Package into a JAR
mvn package

# Clean build artifacts
mvn clean

# Full clean build + test
mvn clean package
```

There are no custom shell scripts or Makefile targets — standard Maven lifecycle phases cover everything.

---

## Running the Application

After building, run the compiled JAR:

```bash
cd test111
mvn package
java -cp target/test-0.0.1-SNAPSHOT.jar org.alexi.javabrains.test.App
# Output: Hello World!
```

---

## Testing Conventions

- Test classes extend `junit.framework.TestCase` (JUnit 3 style — no annotations).
- Test methods must be named with the `test` prefix (e.g., `testApp()`).
- A static `suite()` method aggregates tests via `TestSuite`.
- All tests live under `src/test/java/` mirroring the main source package structure.

Example pattern:

```java
public class AppTest extends TestCase {
    public static Test suite() {
        return new TestSuite(AppTest.class);
    }

    public void testApp() {
        assertTrue(true);
    }
}
```

Do **not** introduce JUnit 4/5 annotations (`@Test`, `@Before`, etc.) unless the dependency in `pom.xml` is updated first.

---

## Code Conventions

- **Package:** `org.alexi.javabrains.test` — keep all new classes in this package.
- **Brace style:** Opening brace on its own line (Allman style), matching the existing `App.java`.
- **JavaDoc:** Add class-level JavaDoc comments for new classes.
- **No external dependencies** in the main (non-test) compile scope — keep it dependency-free unless explicitly requested.

---

## Git Workflow

- **Default branch:** `master`
- **Feature/AI branches:** prefixed with `claude/` (e.g., `claude/claude-md-mm8kpjq2osy3m2wg-WdmIA`).
- GPG commit signing is enabled via SSH key.
- Push commands: `git push -u origin <branch-name>`

Commit message language: Spanish (matching existing history), but English is acceptable for AI-generated commits.

---

## Key Files at a Glance

| File | Purpose |
|------|---------|
| `test111/pom.xml` | Maven build config, dependency versions, packaging |
| `test111/src/main/java/.../App.java` | Application entry point |
| `test111/src/test/java/.../AppTest.java` | Unit test suite |
| `README.md` | Human-facing project description |
| `test.txt` | Plain text sample file (not build-related) |

---

## What to Avoid

- Do not modify `test.txt` unless explicitly asked — it is a sample artifact, not source code.
- Do not upgrade JUnit without updating `pom.xml` and refactoring tests to match the new API.
- Do not push to `master` directly — use a feature/AI branch and open a pull request.
- Do not add unnecessary dependencies to the main compile scope.
