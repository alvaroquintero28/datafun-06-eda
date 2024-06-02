## Step 1. Create a GitHub Repo with README.md
Go to GitHub and create a new GitHub repo in your browser for Project 6 (use the name the specification requires). Be sure to add a default README.md when you first create the repository - it makes the easiest workflow.
## Step 2. Clone Repo
Copy the URL of your new GitHub repo into your clipboard (CTRL+A, then CTRL+C, or CMD if on Mac).
Open a Git Bash, Terminal, or PowerShell terminal in your Documents folder (the parent folder of where you want your repo) and type:  git clone paste_your_repo_URL_here
## Step 3.  Create a Project Virtual Environment
python3 -m venv .venv
## Step 4. Activate Project Virtual Environment
source .venv/bin/activate
## Step 5. Manage Your Project Requirements
## Step 6. Git Add and Commit Your Changes
.venv/
.gitignore - see the spec .gitignore for suggested contentsLinks to an external site. 
.venv/
.ipynb_checkpoints/
README.md
requirements.txt
git add .
git commit -m "initial commit"
## Step 7. Git Push To GitHub
git push origin main
## Choose Your Data Set
Choose one of the data sets and use it to practice all the skills that go into a Python Exploratory Data Analysis project. 
## Document Your Data Set
Add a description of your dataset and a clickable link to your README.md file. Choose one of the following options. 
Option 1. Add Dataset Description & Link Locally - the Easy, Safe Way
Edit your README.md on your machine using VS Code, and git add, commit, and push your data addition to the GitHub repository. If you always edit on your machine, it's easy to keep things in sync with git add/commit/push and avoid dreaded merge conflicts.
