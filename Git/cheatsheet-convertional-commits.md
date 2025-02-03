## Cheatsheet für Conventional Commits

Conventional Commits bieten eine standardisierte Methode, um Git-Commit-Nachrichten klar und strukturiert zu gestalten. Dies verbessert die Lesbarkeit, Nachvollziehbarkeit und Automatisierung (z. B. Changelog-Generierung oder semantische Versionierung). Hier ist ein Überblick über die wichtigsten Regeln und Beispiele.

### **Grundstruktur**

```
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]
```

- **`<type>`**: Der Typ des Commits (z. B. `feat`, `fix`).
- **`[optional scope]`**: Ein optionaler Bereich, der den betroffenen Teil des Projekts beschreibt (z. B. `api`, `ui`).
- **`<description>`**: Eine kurze Beschreibung der Änderung.
- **`[optional body]`**: Detaillierte Beschreibung der Änderung (z. B. Motivation, Kontext).
- **`[optional footer(s)]`**: Zusätzliche Informationen wie Breaking Changes oder Referenzen zu Issues.

---

### **Commit-Typen**

| Typ          | Beschreibung                                                                      | Beispiel                                                   |
| ------------ | --------------------------------------------------------------------------------- | ---------------------------------------------------------- |
| **feat**     | Fügt eine neue Funktion hinzu.                                                    | `feat(parser): add JSON parsing support`                   |
| **fix**      | Behebt einen Fehler.                                                              | `fix(auth): resolve login issue with expired tokens`       |
| **docs**     | Änderungen an der Dokumentation (z. B. README).                                   | `docs(readme): update installation instructions`           |
| **style**    | Änderungen, die das Format betreffen (keine Logikänderungen).                     | `style(css): fix indentation in styles.css`                |
| **refactor** | Codeänderungen, die weder Fehler beheben noch neue Features hinzufügen.           | `refactor(core): simplify data processing logic`           |
| **test**     | Hinzufügen oder Anpassen von Tests.                                               | `test(api): add unit tests for user endpoint`              |
| **chore**    | Wartungsarbeiten, die keine Quellcodeänderungen betreffen (z. B. Build-Prozesse). | `chore(deps): update dependency versions`                  |
| **perf**     | Änderungen zur Verbesserung der Performance.                                      | `perf(image-rendering): optimize image loading time`       |
| **build**    | Änderungen am Build-System oder externen Abhängigkeiten.                          | `build(webpack): update webpack to v5`                     |
| **ci**       | Änderungen an CI-Konfigurationen (z. B. GitHub Actions).                          | `ci(actions): add caching for dependencies in CI pipeline` |
| **revert**   | Rückgängigmachen eines früheren Commits.                                          | `revert: revert "feat(parser): add JSON parsing support"`  |

---

### **Breaking Changes**

Wenn eine Änderung nicht abwärtskompatibel ist, wird dies im Commit hervorgehoben:

- Füge ein Ausrufezeichen (`!`) nach dem Typ oder Scope hinzu.
- Beschreibe die Breaking Change im Footer.

Beispiel:

```
feat(api)!: change response format to JSON

BREAKING CHANGE: The API response format has been changed from XML to JSON.
```

---

### **Best Practices**

1. Schreibe Commit-Nachrichten in der Gegenwartsform und aktiv:
   - Gut: `fix(auth): resolve login issue`
   - Schlecht: `fixed auth issue`
2. Halte die erste Zeile unter 50 Zeichen und beschreibe prägnant.
3. Trenne den Body mit einer Leerzeile und nutze ihn für Details.
4. Verweise auf Issues oder Tickets im Footer:
   ```
   Closes #123
   ```

---

### **Beispiele**

1. Neue Funktion hinzufügen:
   ```
   feat(ui): add dark mode toggle
   ```
2. Fehler beheben:
   ```
   fix(api): handle null values in response
   ```
3. Dokumentation aktualisieren:
   ```
   docs(changelog): add release notes for v1.2
   ```
4. Breaking Change einführen:

   ```
   refactor(core)!: remove deprecated methods

   BREAKING CHANGE: The methods X and Y have been removed due to deprecation.
   ```

---

### **Tools zur Unterstützung**

- **Linting:** [Commitlint](https://commitlint.js.org/) prüft Commit-Nachrichten auf Einhaltung der Konventionen.
- **Automatische Changelog-Generierung:** Tools wie [standard-version](https://github.com/conventional-changelog/standard-version) oder [semantic-release](https://semantic-release.gitbook.io/semantic-release/).
- **Git-Hooks:** Mit [Husky](https://typicode.github.io/husky/) können Commit-Nachrichten vor dem Speichern überprüft werden.
