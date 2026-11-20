# AI Showcase — How JetBrains tools powered this build

> Cloud Rider — a Cloud9 booth mini-game for the Cloud9 x JetBrains
> "Sky's The Limit" Hackathon 2026, Category 3 (Event Mini Game).

## The JetBrains tool used

**IntelliJ IDEA Community Edition 2025.3** (free, no account, no trial),
downloaded from the official JetBrains release API
(`https://download.jetbrains.com/idea/idea-2025.3.tar.gz`, 1.5 GB tarball,
SHA-verified by extracting it successfully) and run on a Linux VM.

We deliberately chose the **free Community Edition** over a WebStorm trial:
a trial would have required a JetBrains account login in a browser, and the
Community Edition already covers everything this single-file HTML5 game needs
— HTML/CSS/JS editing with syntax highlighting, inspections, and Git integration.

## What the IDE actually did

1. **Opened the real project.** The repository folder was opened in IDEA
   (`File > Open`), the User Agreement accepted, data sharing declined,
   and the project trusted. The Project tool window shows the whole repo:
   `index.html`, `README.md`, `LICENSE`, `screenshots/`.
2. **Edited the game in the editor.** The M-key mute toggle was written
   inside IDEA's editor, not in another tool:
   - `Ctrl+F` found the `window.__game` test hook at the end of the script.
   - A new `keydown` listener was added just above it:

     ```js
     // M toggles sound (added in IntelliJ IDEA)
     window.addEventListener("keydown", e => {
       if ("mM".includes(e.key)) {
         soundOn = !soundOn;
         $("soundBtn").textContent = soundOn ? "Sound: on" : "Sound: off";
       }
     });
     ```

     (Committed as a single line in the file; the multi-line form above is
     the same code, formatted for readability.)
   - IDEA's inspections flagged the one real error introduced along the way
     (a stray character), and the file was corrected in the editor until
     the editor showed **0 errors** and `node --check` passed on the
     extracted script.
3. **Git integration.** The IDE's Git tool window shows the project on branch
   `main`; the edit was committed and pushed from the terminal after the
   in-IDE save (`Ctrl+S`).
4. **Verified in the IDE's own view.** The final screenshot in
   `screenshots/idea.png` shows the project open in IDEA with the new
   listener visible at the end of `index.html`.

## What the IDE did not do

- No AI code generation was used: every line of the game was written by a
  human (well — by the developer driving the keyboard) and reviewed in the
  editor. IDEA's role was editing, navigation, inspection, and project
  management — the honest, everyday JetBrains workflow.
- No Junie and no JetBrains AI were involved in this build.

## The workflow in one sentence

Write the game, open it in IntelliJ IDEA Community, use Find to jump to the
right spot, edit with the editor's inspections watching your back, save,
verify with `node --check` and a headless-Chrome playtest, commit.

That is the whole AI-powered workflow story: a free JetBrains IDE, used
genuinely, for the entire edit-test loop of a booth game.
