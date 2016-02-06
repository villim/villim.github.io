---
layout: post
title: SVN Branching Commands
tags: Svn

---

Source control is not just for store source code into code base. Treat it as database is totally wrong! 

Infact, Using it well can greatly enhance your efficiency. Try to commit as many as possible, it will save your effort when power down. Try to remove all unsed lines and never thinking it maybe used later will help making your code more understandable and easiler for other people to pair with you. The commit history also very helpful to review your own work.

Trunk is the usually the reliable and workable source base for release. We should make sure it's always releasable, so we'd better create Branch for our own story.

** The following instruction is based on command line. You can also easy do the same thing in TortoiseSVN. **

** Following commands require your SVN client and server is greater than 1.7 **

### Hints

You can easily get **[trunk-url]** by
```bash
cd [trunk-working-copy-path]
svn info
```

### Create branch:
```bash
svn copy [trunk-url] [branch-url] -m "{story-id} create branch" 
```

### Merge from trunk to branch

While you working on Branch, Trunk is updated. You should merge from trunk ASAP

(1) Make sure you don't have local modification
```bash
cd [branch-working-copy-path]
svn status 
```

(2) Update before merge
```bash
svn update
```

(3) While merging there may have confilicts, chose POSTPONE to solve them later
```bash
svn merge [trunk-url]
```

(4) After solve conflicts, commit
```bash
svn commit -m "merge from trunk" 
```

### Merge from Branch to Trunk

Before merge branch to trunk, make sure **merge from to branch** to let branch code contains latest trunk changes.

(1) Make sure you don't have local modification
```bash
cd [trunk-working-copy-path] 
svn status 
```

(2) Update before merge
```bash
svn update
```

(3) Encounter confilicts during merge, just trust Branch's version
```bash
svn merge --reintegrate [branch-url]
```

(4) This commit reversion is [latest-merge-reversion-of-turnk] for later use
```bash
svn commit -m "merge from branch for {story-id} "   
```

(5) If merge failed, you can revert by
```bash
svn revert -R [trunk-working-copy-path]
```

### Continue Working on a Merged Branch

After branch merge into trunk, there would be conflicts when you merge the second time. So we have to do record only to avoid confilicts.
 
(1) Make sure you don't have local modification
```bash
cd [branch-working-copy-path]
svn status
```

(2) Update before merge
```bash
svn update
```

(3) Record only merge
```bash
svn merge --record-only -c [latest-merge-reversion-of-turnk] [trunk-url]
svn commit -m "record only at reversion {latest-merge-reversion-of-turnk} " 
```
 
(4) Then you can just get latest trunk changes as before
```bash
svn merge [trunk-url]
svn commit -m "merge from trunk after record only"
```