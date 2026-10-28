# vale_vocab

**Centralized Git repository for Vale vocabularies.**

This repository stores **custom vocabularies** for [Vale](https://vale.sh/), organized in **dedicated folders**, all on the `main` branch. Each folder represents a **vocabulary** (e.g., `rockydocs`, `neovim`, `python`) and contains its `accept.txt` and `reject.txt` files.

This structure is designed to work seamlessly with **[nvim-vale-tools](https://framagit.org/ambaradan/nvim-vale-tools)**, a Neovim plugin for managing Vale configurations and vocabularies.

## 📌 Features

- **Single repository**: A single Git repository has all vocabularies.
- **Folder-based organization**: Each vocabulary is a folder on `main` — browsable directly from the GitHub web UI and indexed by search.
- **Per-vocabulary documentation**: Each folder can include its own `README.md` alongside the term files.
- **Seamless synchronization**: Use `nvim-vale-tools` to install, update, or push vocabularies directly from Neovim.

## 🗂️ Repository structure

The repository follows this structure (all on `main`):

```text
vale_vocab/ (repository, main branch)
├── README.md          # This index
├── rockydocs/         # rockydocs vocabulary
│   ├── README.md      # Optional: vocabulary documentation
│   ├── accept.txt     # Terms to accept
│   └── reject.txt     # Terms to reject
├── neovim/
│   ├── accept.txt
│   └── reject.txt
└── ...
```

### Key rules

1. **Folder name = Vocabulary name**: each vocabulary lives in a folder named exactly like the vocabulary itself.
2. **`accept.txt` and `reject.txt` are mandatory**: each vocabulary folder must contain both files.
3. **Root stays clean**: no `accept.txt`/`reject.txt` at the repository root.
4. **Vocabulary-only folders**: each folder contains the term files and (optionally) a `README.md` — nothing else.

## 📥 How to use with [nvim-vale-tools](https://framagit.org/ambaradan/nvim-vale-tools)

### 1. Install a Vocabulary

To install a vocabulary from this repository in Neovim, use:

```vim
:ValeVocab git add git@github.com:ambaradan/vale_vocab.git rockydocs
```

- This clones the repository, copies `rockydocs/accept.txt` and `rockydocs/reject.txt` to Neovim's data directory (`stdpath("data")/vale-tools/styles/config/vocabularies/rockydocs/`), and registers the vocabulary in `.vale.ini`.

### 2. Update a Vocabulary

To update a vocabulary to the latest version:

```vim
:ValeVocab git update rockydocs
```

- This clones the repository again and overwrites the local files with the current version of the folder.

### 3. Update all vocabularies

To update all vocabularies installed from this repository:

```vim
:ValeVocab git update-all
```

### 4. Delete a Vocabulary

To delete a vocabulary:

```vim
:ValeVocab git del rockydocs
```

- This removes the local vocabulary and its metadata.

### 5. Push local changes

If you modify `accept.txt` or `reject.txt` locally and want to push the changes back to the repository:

```vim
:ValeVocab git push rockydocs
```

- This commits and pushes your changes to the `rockydocs/` folder on `main`.

## 🛠️ Manual Usage (Without nvim-vale-tools)

If you want to use this repository **without** the Neovim plugin, follow these steps:

### 1. Clone the repository

```bash
git clone git@github.com:ambaradan/vale_vocab.git
cd vale_vocab
```

### 2. Copy files to Vale's styles directory

Copy the vocabulary folder (e.g., `rockydocs/`) to Vale's `StylesPath` (default: `~/.local/share/vale/styles/config/vocabularies/`):

```bash
cp -r rockydocs/ ~/.local/share/vale/styles/config/vocabularies/
```

### 3. Update `.vale.ini`

Add the vocabulary to your `.vale.ini`:

```ini
Vocab = Vale, rockydocs
```

## 📝 How to contribute

We welcome contributions! Here's how you can help:

### 1. Add a new Vocabulary

1. **Create a new folder** with the name of your vocabulary (e.g., `rust`):

    ```bash
    mkdir rust
    ```

2. **Add `accept.txt` and `reject.txt`** to the folder:

    ```bash
    touch rust/accept.txt rust/reject.txt
    ```

3. **Populate the files** with your terms (one term per line).
4. **Commit and push** (a feature branch + pull request is welcome for larger additions):

    ```bash
    git add rust/
    git commit -m "Add Rust vocabulary"
    git push origin main
    ```

### 2. Update an existing Vocabulary

1. Make your changes to the vocabulary's `accept.txt` or `reject.txt`.
2. Commit and push:

    ```bash
    git add rockydocs/
    git commit -m "Update rockydocs vocabulary"
    git push origin main
    ```

## 📌 Vocabulary guidelines

### General rules

- **One term per line**: each line in `accept.txt` or `reject.txt` should contain a single term.
- **No duplicates**: avoid duplicate terms in the same file.
- **Lowercase by default**: write terms in lowercase unless you need case sensitivity.
- **Comments**: use `#` to add comments (e.g., `# rockydocs-specific terms`).

### Example `accept.txt`

```text
# Accepted terms for rockydocs
rocky
Rocky Linux
dnf
rpm-ostree
kickstart
```

### Example `reject.txt`

```text
# Rejected terms for rockydocs
rhel
centos
```

## 🔍 Vocabulary naming conventions

- Use **lowercase** for vocabulary names (e.g., `rockydocs`, `neovim`, `python`).
- Use **hyphens** for multi-word names (e.g., `c-sharp`, `data-science`).
- Avoid spaces or special characters.

## 📜 License

This repository uses the MIT License. See [LICENSE](LICENSE) for details.

## 🙌 Acknowledgments

- Thanks to [Vale](https://vale.sh/) for the amazing linter.
- Thanks to [nvim-vale-tools](https://framagit.org/ambaradan/nvim-vale-tools) for the seamless integration with Neovim.