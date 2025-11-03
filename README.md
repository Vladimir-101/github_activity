This guide will help you practice using **Git** and **GitHub** — from setting up a local repository to collaborating with others.  
We’ll use a simple HTML project as an example.

---

## Part A — Setting Up Your Local Repository

1️ **Create a demo project folder:**
```bash
mkdir github-activity
cd github-activity
echo "<h1>Hello GitHub!</h1>" > index.html

2 ##Initialize Git and make your first commit:

bash

git init
git status                 # Check your files
git add .                  # Stage all files
git commit -m "feat: initial commit with index.html"
git log --oneline          # Check your commit history

## Part B -- Connect and Push To Github
1 Create a new Github repo (name it github-activity)
don't add a README.md or .gitignore yet.

2 Connect your local repo and push your code.

bash

git branch -M main
git remote add origin https://github.com/<your-username>/github-activity.git
git push -u origin main

 If you get an error because the GitHub repo already has commits (like a README):

bash

git pull --rebase origin main
git push -u origin main

 Part C — Working in Branches (Collaboration)

This is how developers work together without breaking the main branch.

1️ Create a new branch for your feature:

git switch -c feature/add-style

2️ Make some changes and commit:

bash

echo "h1 { color: blue; font-family: system-ui; }" > style.css
echo '<link rel="stylesheet" href="style.css">' >> index.html

git add .
git commit -m "style: added a simple CSS file"

3️ Push your branch to GitHub:

bash

git push origin feature/add-style

4️ Go to GitHub → Open a Pull Request (PR)

Compare feature/add-style → main, write a short title/description, and click Merge when ready. 

5️ Update your main branch after merging:

bash
git switch main
git pull origin main


 Part D — Staying Updated (Pull, Fetch, Merge)

Keep your project synced with your teammates’ changes.

Pull latest changes:

bash
git pull origin main

Fetch changes (view only, no merge yet):

bash
git fetch origin
git log --oneline HEAD..origin/main

Merge main into your current branch:

bash
git switch feature/add-style
git merge main
# Fix any conflicts if needed
git add .
git commit -m "chore: resolved merge conflicts"

Tip: You can also use git rebase main for a cleaner history (advanced users).

Part E — .env Files & .gitignore
What is a .env file?

A .env file stores private information (like passwords or API keys) used by your app.

Example .env:

ini
# Do not upload real credentials!
DATABASE_URL=postgres://user:pass@localhost:5432/app_db
API_KEY=12345SECRET

How to make sure .env is ignored by Git

Create a file named .gitignore and add this:

bash
# Ignore environment and config files
.env
*.env
*.local
*.key

# Ignore system and editor files
.DS_Store
.vscode/
.idea/

Check:

bash
git status  # .env should not appear


If you already committed .env by mistake:

bash
git rm --cached .env
git commit -m "chore: removed .env from tracking"
git push
