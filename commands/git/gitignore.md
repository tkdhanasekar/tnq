## gitignore

Step 1: Create a demo project
mkdir gitignore-demo
cd gitignore-demo
git init


Repository:

gitignore-demo/

Step 2: Create some files
touch app.js
touch .env
mkdir node_modules
touch node_modules/package.json
touch app.log


Repository:

gitignore-demo/
│── app.js
│── .env
│── app.log
└── node_modules/
    └── package.json

Step 3: Check Git status
git status


Output:

Untracked files:
    .env
    app.js
    app.log
    node_modules/


Git wants to track everything.

Step 4: Create .gitignore
touch .gitignore


Add the following:

# Ignore environment files
.env

# Ignore logs
*.log

# Ignore dependencies
node_modules/

Step 5: Check status again
git status


Output:

Untracked files:
    .gitignore
    app.js


Notice that:

✅ app.js is still visible.
❌ .env is ignored.
❌ app.log is ignored.
❌ node_modules/ is ignored.
Step 6: Add tracked files
git add .
git commit -m "Initial commit"


Now only these files are committed:

gitignore-demo/
│── .gitignore
└── app.js

Step 7: Verify ignored files

Run:

git status


Output:

On branch master
nothing to commit, working tree clean


Even though .env, app.log, and node_modules/ exist, Git ignores them.

Step 8: What if you accidentally committed .env first?

Suppose you did this before creating .gitignore:

git add .
git commit -m "Added everything"


Then later you create:

.env


Run:

git status


Modify .env:

echo "API_KEY=123" > .env
git status


Output:

modified: .env


Why? Because .env is already tracked.

Step 9: Stop tracking the file
git rm --cached .env
git commit -m "Stop tracking .env"


Now:

git status


Output:

nothing to commit, working tree clean


The file still exists on your computer but is no longer tracked by Git.

Final repository
gitignore-demo/
│── .gitignore      ✅ Tracked
│── app.js          ✅ Tracked
│── .env            ❌ Ignored
│── app.log         ❌ Ignored
└── node_modules/   ❌ Ignored

Summary of commands
mkdir gitignore-demo
cd gitignore-demo
git init

touch app.js .env app.log .gitignore
mkdir node_modules
touch node_modules/package.json

# Add ignore rules to .gitignore
echo ".env" >> .gitignore
echo "*.log" >> .gitignore
echo "node_modules/" >> .gitignore

git status
git add .
git commit -m "Initial commit"

# If .env was already committed
git rm --cached .env
git commit -m "Stop tracking .env"


This demo illustrates the most common real-world scenario: tracking source code while ignoring secrets (.env), log files, and installed dependencies.
