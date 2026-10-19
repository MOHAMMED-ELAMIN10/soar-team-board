# SOAR Team Board

A live task board for the SOAR graduation project team. It shows tasks, each member's progress, and the plan phases A–J from the Team Handbook. It runs on GitHub Pages. The shared data is stored in this repository, and every change is saved as a commit, so the full history is on GitHub.

- **Overview**: project progress, a card for each member, phase progress, tasks due soon or overdue, and recent activity.
- **Board**: To do / In progress / Done, with search and filters. From a card you can change the status, postpone (+1 day, +3 days, +1 week, or a chosen date), edit, or delete.
- **Plan**: the handbook plan, phase by phase, with each task's "Done when" check.
- **Settings**: everything can be edited, including the project title, Week 1 date, members (name, track, GitHub username), and phases (code, name, timing, dates, order). It also has JSON backup and restore.

## One-time setup (repository owner, about 5 minutes)

1. Create a **public** repository on GitHub, for example `soar-team-board`.
2. Select **Add file → Upload files**, then drag in `index.html`, `README.md`, and the `data` folder (it contains `board.json`). Commit to `main`.
3. Go to **Settings → Pages**. Under *Build and deployment*, set **Source: Deploy from a branch**, **Branch: main**, **Folder: / (root)**, and select **Save**. After about a minute, the site is at
   `https://<your-username>.github.io/soar-team-board/`
4. Go to **Settings → Collaborators → Add people** and invite the other five members. Each member must accept the invitation.

## For each member (once per device)

1. Open the site and select **Connect GitHub**.
2. Follow the link to create a *classic* personal access token. The `public_repo` scope is pre-selected; set the expiration to the end of the project. Copy the token and paste it on the site.
3. Choose your name under **You are**. If your GitHub username is saved in Settings → Team members, your name is chosen automatically.

Anyone with the link can **view** the board without a token. Only collaborators who have connected can **edit**.

## How it works

- The shared data is `data/board.json` on the `board-data` branch. That branch is created automatically on the first change. Keeping the data on its own branch stops edits from triggering GitHub Pages rebuilds.
- The copy of `data/board.json` on `main` is only the starting plan imported from the handbook. After the first change, edit the board through the site, not this file.
- Open pages check for changes every 20 seconds (every 2 minutes for viewers without a token), and immediately when the tab comes back into focus.
- If two people save at the same moment, the second save is replayed on top of the first, so neither change is lost.
- Change history: `https://github.com/<owner>/<repo>/commits/board-data/data/board.json`. To undo a change, use **Settings → Import JSON** with an export, or revert the commit on GitHub.
- The token is stored only in each member's browser (localStorage). It is sent only to `api.github.com`.

## Hosting somewhere other than GitHub Pages

Set `owner` and `repo` in the `BOARD_CONFIG` block near the top of `index.html`, or open the page with `?repo=OWNER/REPO` added to the address.
