# Smart Reordering — Group Work Tutorial

This guide explains how to submit your two researched Smart Reordering features to the group's GitHub repository.

## Before You Start

You should already have:

- A GitHub account
- Git installed if using the command line
- One working GitHub authentication method:
  - GitHub Desktop, or
  - Git + SSH
- Your Git name and email configured correctly

**Repository:** `Emmanuel-Essien/inventory-management-basic`

**Working branch:** `Smart_Reordering_group_work`

> **Do not make your changes on `main`.**

## What You Are Submitting

Each member researches **two independent Smart Reordering features**.

For each feature:

1. Create one Markdown file.
2. Use this filename format:
   `Smart_Reordering_<Feature_Name>.md`
3. Use the feature template in this `tutorial` folder.
4. Complete the research and include your sources.

Each member submits **two feature files in one commit**.

Example:

```text
Smart_Reordering_Demand_Forecasting.md
Smart_Reordering_Reorder_Point.md
```

Commit message:

```text
Add Smart Reordering features: Demand Forecasting and Reorder Point
```

## Option A — GitHub Desktop

### 1. Sign in

Open GitHub Desktop and sign in to **your own GitHub account**.

### 2. Clone the group's repository

Choose **Clone a repository** and use:

```text
https://github.com/Emmanuel-Essien/inventory-management-basic.git
```

Choose where you want the repository stored and clone it.

### 3. Switch to the group branch

Use the branch selector and select:

```text
Smart_Reordering_group_work
```

Make sure this is the branch shown before you begin editing.

### 4. Create your two files

Copy the feature template twice and rename the copies using the required format.

Complete both files.

### 5. Review your changes

In GitHub Desktop, check that only your intended two feature files are changed.

### 6. Commit both files together

Use one commit for both features.

Example:

```text
Add Smart Reordering features: Demand Forecasting and Reorder Point
```

### 7. Push

Click **Push origin**.

Your two files and your commit should now be on the group's branch.

---

## Option B — Git + SSH

### 1. Make sure SSH works

Run:

```bash
ssh -T git@github.com
```

You should receive a successful-authentication message.

### 2. Clone the group's repository

Run:

```bash
git clone git@github.com:Emmanuel-Essien/inventory-management-basic.git
cd inventory-management-basic
```

### 3. Switch to the group branch

Run:

```bash
git switch --track origin/Smart_Reordering_group_work
```

If the branch already exists locally:

```bash
git switch Smart_Reordering_group_work
```

Verify:

```bash
git branch
```

The active branch should be:

```text
* Smart_Reordering_group_work
```

### 4. Create your two feature files

Copy the feature template twice and rename the copies.

Example:

```text
Smart_Reordering_Demand_Forecasting.md
Smart_Reordering_Reorder_Point.md
```

Complete both files.

### 5. Check your Git identity

Before committing:

```bash
git config user.name
git config user.email
```

These should identify **you**.

For a shared laptop, use repository-specific settings:

```bash
git config user.name "Your Full Name"
git config user.email "your-email@example.com"
```

Use an email address associated with your GitHub account.

### 6. Review your files

Run:

```bash
git status
```

Make sure the two feature files are the files you intend to submit.

### 7. Stage both files

```bash
git add Smart_Reordering_Feature_1.md Smart_Reordering_Feature_2.md
```

Replace the example names with your actual filenames.

### 8. Commit both features together

```bash
git commit -m "Add Smart Reordering features: Feature 1 and Feature 2"
```

Replace the feature names with your actual feature names.

### 9. Push

```bash
git push origin Smart_Reordering_group_work
```

Your two files should now be on the group's branch.

---

## Shared Laptop

If you are using someone else's laptop:

1. Use **your own GitHub account**.
2. Do not use the laptop owner's GitHub account.
3. Check the Git name and email before committing.
4. Make your two feature files.
5. Commit both features in one commit.
6. Push your work.
7. Sign out of GitHub Desktop/remove your account from the shared machine when finished.

Do not give anyone your GitHub password or private SSH key.

The shared-laptop arrangement is only a temporary solution for this assignment. Regular access to a computer will become increasingly important when the coursework moves into actual Java/C programming and larger development work.

---

## Important Rules

### 1. Two features = two Markdown files = one commit

Each member submits their two researched features together in one commit.

### 2. Use your own GitHub account

Your contribution must be made from your own account.

### 3. Check your Git identity

Your `user.name` and `user.email` must identify you before you commit.

### 4. Do not work directly on `main`

Use:

```text
Smart_Reordering_group_work
```

### 5. Do not edit the template itself

Copy it and rename the copy.

### 6. Keep the research independent

Do not post your proposed features in the group chat during the research stage.

---

## If Something Goes Wrong

### Permission denied / cannot push

Check that:

- You have accepted the invitation to the group repository.
- You are authenticated to the correct GitHub account.
- Your remote points to the group's repository.

Check:

```bash
git remote -v
```

It should point to:

```text
git@github.com:Emmanuel-Essien/inventory-management-basic.git
```

or the equivalent HTTPS URL.

### Your file is missing

Check your branch:

```bash
git branch
```

You should be on:

```text
Smart_Reordering_group_work
```

### Push rejected because the remote has newer changes

Someone else may have pushed before you.

Run:

```bash
git pull --rebase origin Smart_Reordering_group_work
```

Then:

```bash
git push origin Smart_Reordering_group_work
```

If Git reports a conflict, stop and ask the group leader for help.

### Git shows the wrong name or email

Check:

```bash
git config user.name
git config user.email
```

Then correct the repository-specific values:

```bash
git config user.name "Your Full Name"
git config user.email "your-email@example.com"
```

Use an email address associated with your GitHub account.

---

## Final Check

Before pushing, confirm:

```text
[ ] I researched two Smart Reordering features.
[ ] I created two Markdown files.
[ ] The filenames follow the required format.
[ ] Both files are complete and include sources.
[ ] I am on Smart_Reordering_group_work.
[ ] My Git name/email identify me.
[ ] I committed both features together.
[ ] I pushed the commit successfully.
```

If something is still not working, send the exact error message and a screenshot of the relevant Git/GitHub screen to the group leader.
