# Software Artifacts Distribution - Team Instructions

This repository is used to share project files, tools, and software artifacts with internal and external stakeholders. Follow the steps below to set up your environment and upload or share files correctly.

---

## Folder Structure

All shared files live inside the `PROJECTS` folder. Each subfolder corresponds to a specific project. Always place files in the correct project folder.

```
PROJECTS/
    BESS/       - Files related to the BESS project
    CASES/      - Files related to the CASES project
    DIU/        - Files related to the DIU project
    Li610/      - Files related to the Li610 project
```

Do not create files directly in the root of the repository or inside the `PROJECTS` folder itself - always go one level deeper into the correct project subfolder.

---

## One-Time Setup

### 1. Install Required Tools

You need the following tools installed before you can contribute to this repository.

| Tool | Download |
|------|----------|
| Git | https://git-scm.com/downloads |
| Git LFS (Large File Support) | https://git-lfs.com |
| VS Code | https://code.visualstudio.com |
| GitHub CLI | https://cli.github.com |

After installing, open a terminal and verify each tool is available:

```bash
git --version
git lfs version
gh --version
```

### 2. Authenticate with GitHub

Open a terminal and run:

```bash
gh auth login -h github.com -p https -s repo -s read:org -s workflow -w
```

Follow the browser prompt to log in with your GitHub account.

After logging in, if the organization requires SSO (Single Sign-On), you will see a `403` error when trying to push. To fix it, run:

```bash
gh api repos/akerwade/Software_Artifacts_Distribution
```

Copy the SSO authorization URL from the error message, open it in your browser, and approve access for the `akerwade` organization. You only need to do this once per machine.

### 3. Configure VS Code for Git LFS

VS Code uses the system Git installation. You need to tell Git LFS to initialize itself so that large files are handled automatically.

Open a terminal in VS Code and run these two commands once per machine:

```bash
git lfs install
```

This configures Git LFS hooks globally. From this point on, any file type tracked by LFS in this repository will be uploaded correctly regardless of size.

### 4. Clone the Repository

```bash
git clone https://github.com/akerwade/Software_Artifacts_Distribution.git
cd Software_Artifacts_Distribution
```

---

## Uploading Files

### Files Under 100 MB

1. Copy or place your file into the correct project subfolder under `PROJECTS/`.
2. In VS Code, open the Source Control panel (left sidebar, branch icon).
3. Stage the file by clicking the `+` icon next to it.
4. Type a short commit message describing the file (e.g. `add Li610 firmware v2.1`).
5. Click the checkmark to commit.
6. Click the `...` menu and select **Push**, or click the sync icon in the bottom status bar.

### Files Over 100 MB (Git LFS Required)

GitHub blocks files larger than 100 MB through regular Git. Git LFS stores the file on GitHub's large file service instead. This repository is already configured to track `.exe` files via LFS. If you need to add other large file types (e.g. `.zip`, `.bin`, `.iso`), run the following command once inside the repo folder:

```bash
git lfs track "*.zip"
git add .gitattributes
git commit -m "track zip files with LFS"
```

Then upload your file the same way as any other file (steps 1-6 above). Git LFS handles the rest automatically.

To see which file types are currently tracked by LFS:

```bash
cat .gitattributes
```

---

## Sharing Files

### Share a Single File (Direct Download Link)

Use this URL pattern to send someone a direct download link to any file in the repository:

```
https://github.com/akerwade/Software_Artifacts_Distribution/raw/main/PROJECTS/<ProjectFolder>/<FileName>
```

**Example** - to share `Absento.exe` from the Li610 project:

```
https://github.com/akerwade/Software_Artifacts_Distribution/raw/main/PROJECTS/Li610/Absento.exe
```

Anyone who clicks this link will immediately download the file. No GitHub account is required since the repository is public.

### Share a Folder (Browse All Files in a Project)

To send someone a link where they can browse and download any file inside a project folder, use this URL pattern:

```
https://github.com/akerwade/Software_Artifacts_Distribution/tree/main/PROJECTS/<ProjectFolder>
```

**Examples:**

| Project | Folder Link |
|---------|-------------|
| BESS | https://github.com/akerwade/Software_Artifacts_Distribution/tree/main/PROJECTS/BESS |
| CASES | https://github.com/akerwade/Software_Artifacts_Distribution/tree/main/PROJECTS/CASES |
| DIU | https://github.com/akerwade/Software_Artifacts_Distribution/tree/main/PROJECTS/DIU |
| Li610 | https://github.com/akerwade/Software_Artifacts_Distribution/tree/main/PROJECTS/Li610 |

The recipient can browse all files in the folder and click any file to download it. No GitHub account is required.

---

## Quick Reference

| Task | Command / Action |
|------|-----------------|
| Pull latest changes | `git pull` |
| See what files changed | `git status` |
| Stage all changes | `git add .` |
| Commit changes | `git commit -m "your message"` |
| Push to GitHub | `git push` |
| Check LFS tracked types | `cat .gitattributes` |
| Track a new large file type | `git lfs track "*.ext"` |
| Re-authenticate with GitHub | `gh auth login -h github.com -p https -w` |

---

## Notes

- Never commit sensitive data (passwords, keys, credentials) to this repository.
- If a push fails with a `403` error, re-run the SSO authorization step described in the setup section above.
- If you accidentally commit a file to the wrong folder, let the repository owner know so it can be moved cleanly without breaking file history.
