# 🐾 Shared Libraries - Guideline

---

## ⚙️ How to get these libraries to your projects?

There are 2 main ways to integrate shared libraries into your projects:

- **Git Submodule** (recommended for reusable, independent libraries)
- **Git Subtree** (recommended for simplicity and ease of use)

---

## 1. Using Git Submodule (be careful because you can make change to this shared repo)

Git submodule allows you to include another repository as a dependency inside your project while keeping it as a separate repo.

### ➕ Add a submodule (specific branch)
```bash
git submodule add -b <branch-name> <repo-url> <path>
```

Example: If you want to get CoreLib from this repository to add to your project at path `Assets/Scripts/SharedLibs`, you can use this command
```bash
git submodule add -b core-lib https://github.com/baotrangia-ctv/SharedLibs.git Assets/Scripts/SharedLibs
```

### 🔄 Initialize & clone project with submodule
```bash
git submodule update --init --recursive
```

### 🔄 Update submodule to latest commit of its branch
```bash
git submodule update --remote
```

📌 Important Notes
- Submodule tracks a specific commit, not a branch
- You must manually update it using git submodule update --remote
- The parent repo stores the exact version of the submodule

✅ Pros
- Clear separation between projects
- Precise version control
- Ideal for shared libraries used across multiple projects

❌ Cons
- More complex workflow
- Requires additional commands
- Can confuse team members unfamiliar with Git

---

## 2. Using Git Subtree (if you are not confident in using git)

Git subtree allows you to embed another repository into your project while keeping the ability to sync changes.

### ➕ Add a submodule (specific branch)
```bash
git subtree add --prefix=<path> <repo-url> <branch> --squash
```

Example: If you want to get CoreLib from this repository to add to your project at path `Assets/Scripts/SharedLibs`, you can use this command
```bash
git subtree add --prefix=Assets/Scripts/SharedLibs https://github.com/baotrangia-ctv/SharedLibs.git core-lib --squash
```

### 🔄 Pull updates
```bash
git subtree pull --prefix=<path> <repo-url> <branch> --squash
```

### 🚀 Push changes back to library repo
```bash
git subtree push --prefix=<path> <repo-url> <branch>
```

📌 Important Notes
- Code becomes part of your repository
- No extra setup needed when cloning
- Use --squash to keep history clean


✅ Pros
- Simple workflow
- No need to manage separate repositories during development
- Works like normal project code

❌ Cons
- Harder to track original source history
- Less strict separation between projects