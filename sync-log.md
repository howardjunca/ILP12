
## Repository

**https://github.com/howardjunca/ILP12.git**

sync-log.md

## How I’d Learn Git as a Beginner

When I started with Git, I first set up my identity so my commits were attributed correctly. Then I learned the basic loop: initialize or clone a repository, make changes, stage them, commit them, and push or pull as needed.

### The First Commands I Learned

| Command | What I use it for |
| :--- | :--- |
| `git config --global user.name "Your Name"` | I set the name that will be attached to my commits. |
| `git config --global user.email "you@example.com"` | I set the email that will be attached to my commits. |
| `git init` | I turn an existing folder into a new Git repository when I’m starting a project from scratch. |
| `git clone <url>` | I create a local copy of an existing remote repository, such as one from GitHub. |
| `git status` | I check which files have changed, which are staged, and which branch I’m on. This is the command I use most often. |
| `git add <file>` or `git add .` | I stage changes and prepare them for the next commit. |
| `git commit -m "Meaningful message"` | I save my staged changes to the repository’s history with a descriptive message. |
| `git log` | I review the commit history, including author, date, and message. |
| `git branch` | I list my local branches and see which one I currently have checked out. |
| `git checkout <branch>` or `git switch <branch>` | I switch to another branch. If I want to create and switch at the same time, I use `git checkout -b <new-branch>`. |
| `git remote add origin <url>` | I link my local repository to a remote one, usually after `git init`. |
| `git push -u origin main` | I upload my local commits to the remote repository for the first time. |
| `git pull origin main` | I fetch the latest changes from the remote and merge them into my local branch. |

### What Works Well for Me

These habits could saved me a lot of confusion:

- **I must commit early and often, with meaningful messages.** I must try to make each commit represent one logical change. Instead of writing `"fixed stuff"`, I write something like `"fix: correct login button alignment"` or `"feat: add user profile page"`.
- **I should use branches for every new feature, bug fix, or experiment.** I avoid working directly on `main`. I create a branch with `git checkout -b feature-x`, do my work there, and merge it back only when it is ready.
- **pull before I push.** Before I start work and before I push my changes, I run `git pull` to incorporate updates from collaborators. This reduces the chance of push rejections and merge conflicts.
- **I check `git status` frequently.** It tells me exactly what Git sees: what is staged, what is modified, and which branch I’m on. It prevents many surprises.
- **I clone via SSH instead of HTTPS when possible.** It avoids repeated authentication prompts and firewall issues, which makes my workflow smoother.

### Problems I Usually Run Into

As a beginner, I commonly ran into the following issues, usually because I misunderstood Git functioning.

#### 1. Misunderstanding repositories: `git init` vs. `git clone`

One of my frequent mistakes was running `git init` inside a folder that I intended to be a clone of an existing project, or trying to clone into a folder that already contained files. I was not understanding that `git init` starts a brand-new history, while `git clone` copies an existing history from a remote. If a folder is not a Git repository, `git status` says `fatal: not a git repository`; I searched and I found I can confirm with `git rev-parse --is-inside-work-tree`.

#### 2. Branch activation confusion

Not knowing which branch I was on led me to commit to the wrong place. Despite warnings mentioned about checking constantly with `git branch` before making changes -I missed that a couple of time- the current branch is marked with an asterisk. If I try to switch branches while I have uncommitted changes, Git may refuse in order to protect my work. In that case, I am not sure what to do yet.

#### 3. Commit mistakes

- **Vague messages:** I wrote `"update"` or `"fix"`, which made history useless. Important to use clear messages like `feat:`, `fix:`, or `docs:`.
- **Committing without configuring identity:** If I haven’t set `user.name` and `user.email`, commits may fail or have incorrect authorship.
- **Huge, messy commits:** A single commit with many unrelated changes is hard to review and revert. I try to keep commits small.

#### 4. Clone problems

- **Authentication failures:** When I clone over HTTPS, GitHub no longer accepts account passwords. I need a **Personal Access Token (PAT)** in place of the password.  Easier with SSH.
- **SSH “Permission denied (publickey)”:** My SSH key was not loaded or not added to my GitHub/GitLab account at the beginning. I test with `ssh -T git@github.com`, add my key to the agent with `ssh-add`, and paste my public key into my account settings.
- **Cloning the wrong URL or wrong branch:** I double-check the repository URL. If I need a specific branch, better  clone with `git clone -b <branch> <url>`.

#### 5. Pull and push problems, what is the right order

- **“Failed to push: rejected (non-fast-forward)” or “remote contains work you do not have locally”:** This means the remote has commits I do not have. I pull first, merge or rebase, and then push again: `git pull origin main` followed by `git push origin main`. Here I have many problems, not completely clear how it works.
- **“Divergent branches” on pull:** Git cannot automatically decide how to extract and summarize local and remote changes. I searched and it must be with `git pull --rebase` but I did not try yet.
- **Pull refuses because of uncommitted local changes:** Git will not overwrite files I have modified but not committed. I commit or stash my changes before pulling.
- **Running `git pull` outside a repository:** If I see `fatal: not a git repository`, I’m probably in the wrong folder. I `cd` into the cloned repository first.

#### 6. Merge conflicts

I read about this possible problem, but I am not at this stage, where different collaborators or branches must be merged.

#### 7. Pull request pitfalls on GitHub/GitLab

A mistake I made was opening a pull request from my `main` branch instead of a branch. I think this can cause problems with tracking changes and branches.

In summary, most of my beginner problems came from not checking `git status` and `git branch` with enough frequency, and from skipping the “pull before push” habit. Building those two reflexes early may prevent future troubles!