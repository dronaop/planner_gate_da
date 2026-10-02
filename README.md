# GATE DA 2027 planner on GitHub Pages

Two files go in the repo: `index.html` (the planner) and `progress.json` (your ticks). Nothing else is needed: no server, no database.

## One-time setup (about 10 minutes)

1. **Sign in to GitHub** with the account you want this to live under.
2. **Create a repo.** New repository → name it `gate-da-planner` → **Public** → Create repository.
3. **Upload the files.** On the empty repo page, click "uploading an existing file", drag in `index.html` and `progress.json`, then **Commit changes**.
4. **Turn on Pages.** Repo **Settings → Pages → Build and deployment → Source: Deploy from a branch → Branch: `main`, folder `/ (root)` → Save.** After about a minute your link appears:
   `https://YOUR-USERNAME.github.io/gate-da-planner/`
5. **Create a token that can only touch this repo.** Profile picture → **Settings → Developer settings → Personal access tokens → Fine-grained tokens → Generate new token**:
   - Token name: `gate planner`
   - Expiration: **Custom**, a date after your exam (fine-grained tokens last up to a year)
   - Repository access: **Only select repositories → `gate-da-planner`**
   - Permissions → Repository permissions → **Contents: Read and write** (GitHub adds "Metadata: Read-only" by itself)
   - Generate, then copy the token (starts with `github_pat_`). GitHub shows it only once.
6. **Sign in on the planner.** Open `https://YOUR-USERNAME.github.io/gate-da-planner/#owner`, paste the token, and press **Sign in**. Do this once on each device or browser you tick from.

Share the link **without** `#owner`. Viewers get a read-only page; there's no sign-in button for them.

## How it works

- **Viewers** load `progress.json` from your public repo through GitHub's API, so they always see the latest ticks. GitHub allows 60 anonymous requests per hour per network. If a viewer goes over that, the page reads the copy GitHub Pages serves instead, which can be a minute or two behind.
- **You:** after you tick, the page waits 2.5 s. Then it fetches the latest `progress.json`, applies your changes and commits. Because it always starts from the latest file, your phone and laptop won't overwrite each other's ticks. Ticks that haven't been saved yet survive a reload or a closed tab.
- **History:** every save is a commit, so the repo's commit list doubles as a study log (for example, "Progress: ticked 3 (D5)").
- **The token** is kept only in that browser's local storage and is sent only to `api.github.com`. It can edit this repo's files and nothing else. The planner rejects a token that belongs to a different GitHub account than the one in the URL. **Sign out** removes it from the device, and you can revoke it anytime on the token settings page.
- **When the token expires,** the page switches to view-only and shows "Token expired · sign in again". Make a new token (step 5) and sign in again.

One caution: all your `*.github.io` project sites share one browser origin, so they can read each other's local storage. Don't host pages you didn't write in your other Pages repos.

## Custom domain or a different layout

If the page isn't served from `YOUR-USERNAME.github.io/REPO/`, fill in `CONFIG` near the top of the script in `index.html` (`owner`, `repo`, and optionally `branch` and `path`).

## Editing the plan

Edit the `DAYS` list in `index.html` on GitHub (pencil icon → commit). Ticks are saved by position (`m_<day>_<i>`, `e_<day>_<i>`, `apt_<day>`). Add new tasks at the end of a session's list. If you insert a task in the middle, the ticks after it shift to the wrong task.
