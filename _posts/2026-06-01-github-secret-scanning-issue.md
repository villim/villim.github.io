---
title: Fix Github Secret Scanning Issue
layout: post
---

![git filter-repo](http://villim.github.io/img/2026/git-filter-repo.jpeg)

Github report  a Secret Scanning issue:

```text
XXX Secret Access Token:

Active secret
GitHub confirmed this secret is active.

pk.xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx ( fake secrect )

Remediation steps
Follow the steps below before you close this alert.
	1 Rotate the secret if it's in use to prevent breaking workflows.
	2 Revoke this xxx Secret Access Token through Mapbox to prevent unauthorized access. Learn more about Mapbox tokens.
	3 Check security logs for potential breaches.
	4 Close the alert as revoked.

```

If we keep the file and remove this Token from the content, Github will re-generate this Alert again later, cause this token still exists in Github history of all the Branches and Tags.  Here is how to fix your Git history:

## Step 1: Install  git-filter-repo

[git-filter-repo](https://github.com/newren/git-filter-repo)  is a versatile tool for rewriting history

```bash
brew install git-filter-repo
```


## Step 2: Clone a fresh copy of your repository

```bash
git clone git@github.com:YOUR_ORG/YOUR_REPO.git
cd YOUR_REPO
```

## Step 3.1: Keep the file and Replace the Token 
We’ll provide git-filter-repo  a replacement file which contains the exact string to be replaced from your history. 

```bash
# Replace the string below with the actual, full token you want to remove 
echo "pk.xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx" > secret-to-remove.txt
```


Navigate to the root directory of your repository (e.g., the root of the ps-avs-init project). Run the following command to scan the entire history and replace the secret with ***REMOVED***.

```bash
git filter-repo --replace-text secret-to-remove.txt

or 

git filter-repo --replace-text secret-to-remove.txt --force
```

*Note:* git-filter-repo *will automatically remove your remote* origin *as a safety precaution after rewriting history.*

This command will scan the entire history, replace the secret string in any commit or file where it appears, and rewrite the repository's history.

## Step 3.2: Delete the file contians Token

If 3.1 replace text is not acceptable, another way is to delete the files contains the Token:

```bash
git filter-repo \
  --path config/secret.properties \
  --path passwords.txt \
  --path .env \
  --invert-paths

or 

git filter-repo --path src/main/resources/ --invert-paths


or 

git filter-repo --path-glob '*.properties' --invert-paths

or

git filter-repo --path-glob '*.secret' --invert-paths --use-base-name

```

* The --invert-paths flag means "keep everything **except** the specified path" — effectively deleting that file from every commit
* The --use-base-name flag matches filenames regardless of directory


## Step 4: Re-add the Remote and Force Push
Because you have rewritten the repository's history, you need to re-add your remote URL and force-push the updated history to GitHub.

```bash
# Re-add your repository's remote URL 
git remote add origin git@github.com:<your-org>/<your-repo-name>.git 

# Force push all branches 
git push origin --force --all
```

*(If you have branch protection rules enabled for your main branch, you may need a repository administrator to temporarily disable them to allow the force push).*

## Step 5: Clean Up and Coordinate

**Delete the temporary file:** Remove the local file containing the plaintext secret.

```bash
rm secret-to-remove.txt
```

**Alert your team:** Anyone else who has pulled the repository recently will have the "poisoned" Git history on their local machine. They should either perform a fresh git clone of the repository or hard reset their local branches to match the remote. If they do a standard git pull or git push, they risk re-introducing the secret into the history.

**Resolve the alert:** Go back to your GitHub Security tab, find the Secret Scanning alert, and mark it as resolved (usually as "Revoked" or "Fixed").





