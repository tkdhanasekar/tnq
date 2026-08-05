A **Pull Request (PR)** in GitHub is a way to propose changes from one branch to another (usually into the `main` branch). It also allows team members to review, comment, and approve your code before it is merged.

Here's the complete workflow with an example.

## Example Scenario

Suppose your repository is:

```
my-app
```

The `main` branch contains:

```python
def greet():
    return "Hello"
```

You want to change it to:

```python
def greet():
    return "Hello, World!"
```

---

## Step 1: Clone the Repository

```bash
git clone https://github.com/username/my-app.git
cd my-app
```

---

## Step 2: Create a New Branch

Never work directly on `main`.

```bash
git checkout -b feature/update-greeting
```

Output:

```
Switched to a new branch 'feature/update-greeting'
```

---

## Step 3: Make Changes

Edit the file.

Before:

```python
def greet():
    return "Hello"
```

After:

```python
def greet():
    return "Hello, World!"
```

---

## Step 4: Check Changes

```bash
git status
```

Output:

```
modified: app.py
```

---

## Step 5: Add Changes

```bash
git add app.py
```

Or add everything:

```bash
git add .
```

---

## Step 6: Commit Changes

```bash
git commit -m "Update greeting message"
```

Output:

```
1 file changed, 1 insertion(+), 1 deletion(-)
```

---

## Step 7: Push the Branch

```bash
git push origin feature/update-greeting
```

Output:

```
Branch 'feature/update-greeting' set up to track remote branch.
```

---

## Step 8: Create the Pull Request (PR)

Go to your repository on GitHub.

You'll usually see a banner like:

```
feature/update-greeting had recent pushes

[Compare & pull request]
```

Click **Compare & pull request**.

Fill in:

**Title**

```
Update greeting message
```

**Description**

```
## What changed
- Updated greeting from "Hello" to "Hello, World!"

## Why
- Improves user-friendly output
```

Click **Create Pull Request**.

Your PR now looks something like:

```
Pull Request #15

Title:
Update greeting message

feature/update-greeting
        ↓
main
```

---

# Step 9: Code Review

A teammate reviews your code.

They may:

* Approve it ✅
* Request changes ❌
* Leave comments 💬

Example comment:

```
Can you add an exclamation mark?
```

---

## Step 10: Make Requested Changes

Modify the code:

```python
def greet():
    return "Hello, World!"
```

to

```python
def greet():
    return "Hello, World!"
```

(Or make whatever change was requested.)

Commit the update:

```bash
git add .
git commit -m "Address review comments"
git push
```

Because you're pushing to the same branch, the existing PR is updated automatically.

---

# Step 11: Reviewer Approves the PR

The reviewer clicks **Approve**.

The PR status changes to:

```
✓ Approved
```

---

# Step 12: Merge (Accept) the Pull Request

Once checks pass and approvals are complete:

Click:

```
Merge pull request
```

Then:

```
Confirm merge
```

GitHub displays:

```
Pull Request Successfully Merged
```

The changes are now part of the `main` branch.

---

# Step 13: Delete the Branch (Optional)

GitHub offers:

```
Delete branch
```

Or from the command line:

```bash
git branch -d feature/update-greeting
git push origin --delete feature/update-greeting
```

---

# Complete Workflow

```text
main
 │
 │
 ├───────────────┐
 │               │
 │      git checkout -b feature/login
 │               │
 │         Make changes
 │               │
 │         git add .
 │               │
 │     git commit -m "Add login"
 │               │
 │ git push origin feature/login
 │               │
 │     Create Pull Request
 │               │
 │        Code Review
 │               │
 │      Reviewer Approves
 │               │
 │      Merge Pull Request
 │               │
 ▼
main (updated)
```

---

# Real Example

Suppose you're fixing a login bug.

```bash
git checkout -b bugfix/login-error

# Edit LoginService.java

git add .

git commit -m "Fix login validation"

git push origin bugfix/login-error
```

On GitHub:

```
Base branch: main
Compare branch: bugfix/login-error

Title:
Fix login validation

Description:
- Fixed null pointer issue
- Added validation
- Updated unit tests
```

A reviewer approves the PR, and you click **Merge pull request** → **Confirm merge**.

---

# Common Git Commands

| Purpose                          | Command                                                                                                         |
| -------------------------------- | --------------------------------------------------------------------------------------------------------------- |
| Clone repository                 | `git clone <repo-url>`                                                                                          |
| Create branch                    | `git checkout -b feature-name`                                                                                  |
| Check status                     | `git status`                                                                                                    |
| Add changes                      | `git add .`                                                                                                     |
| Commit                           | `git commit -m "message"`                                                                                       |
| Push branch                      | `git push origin feature-name`                                                                                  |
| Update branch with latest `main` | `git pull origin main` (or `git fetch` followed by `git rebase origin/main`, depending on your team's workflow) |
| Delete local branch              | `git branch -d feature-name`                                                                                    |
| Delete remote branch             | `git push origin --delete feature-name`                                                                         |

This is the standard workflow used by most teams on GitHub to propose, review, and merge code changes safely.

