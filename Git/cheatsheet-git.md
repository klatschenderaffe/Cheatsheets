Hier ist ein umfassendes **Git und GitHub Cheatsheet** für den schnellen Zugriff auf die wichtigsten Befehle und Funktionen:

## **Grundlegende Konfiguration**

- Benutzername festlegen:  
  `git config --global user.name "Dein Name"`
- E-Mail-Adresse festlegen:  
  `git config --global user.email "deine.email@beispiel.de"`
- Standardeditor definieren:  
  `git config --global core.editor [Editor]`
- Konfiguration anzeigen:  
  `git config --list`

## **Repository erstellen oder klonen**

- Neues Repository initialisieren:  
  `git init [repository-name]`
- Bestehendes Repository klonen:  
  `git clone [URL]`

## **Änderungen verfolgen**

- Status anzeigen:  
  `git status`
- Dateien zum Staging-Bereich hinzufügen:  
  `git add [Dateiname]` oder `git add .` (für alle Änderungen)
- Änderungen anzeigen (vor dem Stagen):  
  `git diff`
- Änderungen im Staging-Bereich anzeigen:  
  `git diff --staged`

## **Commits**

- Änderungen committen:  
  `git commit -m "Commit-Nachricht"`
- Letzten Commit bearbeiten (z. B. Nachricht ändern):  
  `git commit --amend`

## **Branching und Merging**

- Neuen Branch erstellen:  
  `git branch [branch-name]`
- Zu einem Branch wechseln:  
  `git checkout [branch-name]` oder `git switch [branch-name]`
- Branch erstellen und direkt wechseln:  
  `git checkout -b [branch-name]` oder `git switch -c [branch-name]`
- Branch zusammenführen (Merge):  
  `git merge [branch-name]`
- Branch löschen:  
  `git branch -d [branch-name]`

## **Remote-Repositories**

- Remote hinzufügen:  
  `git remote add origin [URL]`
- Änderungen pushen (zum Remote):  
  `git push origin [branch-name]`
- Änderungen pullen (vom Remote):  
  `git pull origin [branch-name]`
- Remote-Daten abrufen, ohne sie zu mergen:  
  `git fetch`

## **Historie und Logs**

- Commit-Historie anzeigen:  
  `git log` oder kompakt mit Einzeilendarstellung:  
  `git log --oneline`
- Änderungen eines bestimmten Commits anzeigen:  
  `git show [commit-hash]`
- Wer hat was geändert? (Datei-Historie):  
  `git blame [Dateiname]`

## **Dateien verwalten**

- Datei löschen und aus Git entfernen:  
  `git rm [Dateiname]`
- Datei umbenennen/verschieben:  
  `git mv [alter-name] [neuer-name]`

## **Rebasing und Reset**

- Rebase aktueller Branch auf einen anderen:  
  `git rebase [branch-name]`
- Letzte Änderungen rückgängig machen (nur lokal):  
  `git reset HEAD~1` (für den letzten Commit)
- Arbeitsverzeichnis komplett zurücksetzen:  
  `git reset --hard`

## **.gitignore**

Erstellen einer `.gitignore` Datei, um bestimmte Dateien oder Ordner zu ignorieren. Beispiel:

```
# Ignoriere Log-Dateien
*.log

# Ignoriere Ordner
/temp/
```

## **Zusammenarbeit auf GitHub**

1. Repository forken (auf GitHub-Webseite).
2. Lokales Repository klonen:
   - `git clone https://github.com/[Benutzername]/[Repository].git`
3. Pull Request erstellen, um Änderungen vorzuschlagen.

Dieses Cheatsheet deckt die häufigsten Szenarien ab und bietet eine solide Grundlage für die Arbeit mit Git und GitHub!

Citations:
[1] https://about.gitlab.com/images/press/git-cheat-sheet.pdf
[2] https://kurse.lerneprogrammieren.de/wp-content/uploads/downloads/freebies/LerneProgrammieren-Git-Cheatsheet.pdf
[3] https://static.javatpoint.com/tutorial/git/download/Git%20Cheat%20Sheet.pdf
[4] https://docs.github.com/en/get-started/getting-started-with-git/git-cheatsheet
[5] https://www.atlassian.com/dam/jcr:8132028b-024f-4b6b-953e-e68fcce0c5fa/atlassian-git-cheatsheet.pdf
[6] https://training.github.com/downloads/de/github-git-cheat-sheet/
[7] https://training.github.com/downloads/github-git-cheat-sheet.pdf
[8] https://education.github.com/git-cheat-sheet-education.pdf
[9] https://home.cit.tum.de/~scfl/summaries/pdf/git.pdf
[10] https://www.teilhabe40.de/fileadmin/user_upload/Dummy_PDFs/git-cheatsheet-EN-grey.pdf
[11] https://wizardzines.com/git-cheat-sheet.pdf

---

Antwort von Perplexity: pplx.ai/share
