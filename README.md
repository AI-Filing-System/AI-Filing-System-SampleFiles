# SampleFiles

SampleFiles is a dedicated repository for **sample and test files used during development**.

This repository is designed to be used as a **Git submodule** by the main project, allowing developers to access necessary test data while keeping the main repository and distributed packages (e.g. pipx / PyPI) lightweight.

Large files and historical test data are **not included in end-user installations**.

---

## Intended Usage

- Used by developers for local development and testing
- Added to the main project as a Git submodule
- Managed using **Git LFS** to avoid bloating Git history
- Not required for runtime or end-user installations

---

# Git LFS Usage Guide

This section summarizes common Git LFS (Large File Storage) commands used in this repository.

---

## 1. Install Git LFS

### macOS
```bash
brew install git-lfs
````

### Ubuntu / Linux

```bash
sudo apt install git-lfs
```

### Initialize Git LFS

```bash
git lfs install
```

> Each developer only needs to run this once per machine.

---

## 2. Track Files with Git LFS

### Track specific file types

```bash
git lfs track "*.pptx"
git lfs track "*.xlsx"
git lfs track "*.docx"
```

### Track an entire folder (including subfolders)

```bash
git lfs track "V1/**"
git lfs track "V2/**"
```

### Verify tracked rules

```bash
cat .gitattributes
```

---

## 3. Add or Modify LFS Files

```bash
git add .gitattributes
git add path/to/large_file.pptx
git commit -m "Add or update files via Git LFS"
git push origin main
```

> Git LFS stores the actual file content on the LFS server, while Git only keeps a lightweight pointer in the repository.

---

## 4. List LFS Files

```bash
git lfs ls-files
```

* Lists all files currently managed by Git LFS.

---

## 5. Pull LFS Files

### After cloning the repository

```bash
git clone https://github.com/your-org/SampleFiles.git
cd SampleFiles
git lfs pull
```

### Using as a submodule

```bash
git submodule update --init --recursive
git lfs pull
```

---

## 6. Remove LFS Files

```bash
git rm path/to/large_file.pptx
git commit -m "Remove file from Git LFS"
git push origin main
```

> Note: This removes the file from Git and LFS tracking going forward.
> Previous commits will still reference historical versions.

---

## 7. Notes and Limitations

1. GitHub Free account LFS limits:

   * 1 GB storage
   * 1 GB bandwidth per month
2. Any change to an LFS-managed file requires:

   * `git add` → `git commit` → `git push`
3. When using this repository as a submodule, developers must explicitly run:

   ```bash
   git lfs pull
   ```

---

## Summary

This repository exists solely to support development and testing workflows.
It intentionally separates large or sample files from the main project to ensure:

* Clean Git history
* Small installation footprint for users
* Predictable and maintainable test data management
