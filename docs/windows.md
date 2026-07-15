# 🪟 Setup guide - Windows

## ⚠️ Requirements: WSL2 + Docker

WSL2 allows running Linux natively on Windows

- ⚡ Native Linux performance without dual boot
- 🔗 Total integration between Windows and Linux
- 🐳 Docker works perfectly
- 🛠️ Development tools run better

On 2004 version of Windows 10 (Home or Professional) and later versions including all Windows 11, WSL is already installed.

---

### Update WSL

To make sure that the most recent version of WSL is running, execute:

```bash
wsl --update
```

---

### Set default WSL version to v2

Normally version 2 is set as default, but sometimes version 1 could be set.

```bash
wsl --set-default-version 2
```

---

### Install Ubuntu

Install `Ubuntu` as default Linux

```bash
wsl --install
```

---

## 📋 What will be configured

1. **[Modern Terminal](#1-modern-terminal)** - Fish or Zsh + Windows Terminal + Fonts
2. **[Docker](#2-docker)** - Containerization and isolated environments
3. **[Essential Tools](#3-essential-tools)** - Neovim, mise, eza, zoxide, fzf
4. **[VSCode](#4-visual-studio-code)** - Professional IDE
5. **[PowerToys](#5-powertoys)** - Utility tools fot Windows

## 1. Modern Terminal

#### 🐟 Fish Shell

**Advantages:**

- ⚡ **Extremely fast**: Rewritten in Rust, maintains performance even after prolonged use
- 🎨 **Live Syntax highlighting**: Colors indicate valid inputs while typing
- 💡 **Intelligent autocomplete**: Context and history based suggestions
- 🔌 **Works out-of-the-box**: Does not need complex initial configuration
- 📝 **Advanced history**: Smart search of previous commands
- 🚀 **Consistent performance**: Does not degrade with time usage

#### Installation

**👉 [Fish Shell - Installation](https://fishshell.com/)** (Follow instructions for Linux/Ubuntu)

#### Plugin: Starship

**Advantages:**

- ⚡Fast and customizable prompts, written in Rust
- 💡Shows Git information, languages, versions
- 🔌Easy to set up

#### Installation

**👉 [Starship - Installation](https://starship.rs/)**

---

### Windows Terminal

Modern Microsoft's Terminal with tabs, themes, GPU acceleration and divisible panels.

**Available versions:**

**🔴 Canary (Suggestion for developers)**

- **Terminal with AI integrated chat**: New feature. Interact with GitHub Copilot directly in the Terminal
  - Just ask "How to do X in git?" and receive immediate answers
  - Generate complex commands explaining what needs to be done
  - Learn tools without exiting the Terminal or opening the browser
- Receives experimental features first
- Installation: [GitHub - Windows Terminal Canary](https://github.com/microsoft/terminal#installing-windows-terminal-canary)
- ⚠️ Might have ocasional bugs, but worth because of the innovations

**🟢 Stable** (Microsoft Store)

- Stable version for the ones who prefer reliability
- Recommended for production usage

**🟡 Preview** (Microsoft Store)

- Features in test phase before going to Stable
- Midway between stability and innovations

### Nerd Font (Required)

To correctly display icons on Fish/Starship:

1. Download **Nerd Font**: [nerdfonts.com/font-downloads](https://www.nerdfonts.com/font-downloads)
2. Install the `.ttf` files
3. Open Windows Terminal → Settings
4. Select **Ubuntu** profile → **Appearance** → In "Font Face" choose **Nerd Font**

### Advanced Settings (Optional)

**Customize via JSON:**

1. Open Windows Terminal → Settings
2. Select **Open JSON File**

**Example File:** [windows-terminal-settings-example.json](../config/windows-terminal-settings-example.json)

- Multiple Themes already configured
- Useful Keybindings
- Optimized default settings

⚠️ **Important:** Keep your own profile GUIDs when copying the example

---

## 2. Docker

Isolated and replicable environments for each project. Simultaneously run multiple Node, Python, PHP, etc. without any issues.

### Installation

Download [here](https://www.docker.com/products/docker-desktop/) and install **Docker Desktop**

After installation is complete, log in with your Docker's account and follow the instructions.

#### Activate Docker in WSL distribution

Access Docker Desktop's panel, click on the gear and then navigate to `Resources -> WSL Integration` and enable the Linus distribution to be used with Docker, then click on `Apply & Restart`

---

## 3. Essential Tools

✨ Multi-platform tools that will improve productivity in the terminal

### Neovim

Modern and extensible text editor, Vim evolution with performance and extensibility focus.

**Features**

- ⚡ Extremely light and fast
- 🔌 Native LSP support (Language Server Protocol)
- 🎨 Rich plugin ecosystem (Lua)
- 🚀 Ideal for fast editions via Terminal
- 💡 Complements VSCode for server tasks

**Installation:**

- **[neovim.io](https://neovim.io/)**

💡 **Tip:** Use Neovim for fast SSH editions and VSCode for local development

**Advanced settings (optional):**

For an IDE-like experience with Neovim:

- [LazyVim](https://www.lazyvim.org/) - Modern pre-configured distribution
- [NvChad](https://nvchad.com/) - Fast and elegant configuration
- [AstroNvim](https://astronvim.com/) - IDE-like with nice patterns

---

### eza

Modern substitute of `ls` command with colors, icons and advanced resources.

**Features**

- 🎨 Colors and icons by default
- 📊 Tree exhibition, grid and long format
- 🔍 Git integration (shows file status)
- ⚡ Developed in Rust - fast and reliable
- 🌳 Integrated file tree visualization

**Installation:**

- **[github.com/eza-community/eza](https://github.com/eza-community/eza)**

**Examples:**

```bash
# List files with icons
eza

# Detailed format with git status
eza -l --git

# Tree visualization
eza --tree

# List all, even hidden files
eza -la
```

**Suggested Aliases:**

```bash
alias lz="eza --color=always --long --no-filesize --icons=always --no-time --no-user --no-permissions"
alias lsz="eza --color=always --long --no-filesize --icons=always --no-time --no-user -la"
alias lt="eza --tree --icons"
```

⚠️ **Important:** Do not substitute common commands like `ls` (ex: `alias ls="eza"`). AI tools like GitHub Copilot and Claude need default output to understand file structure. Create different aliases like como `lz` and `lsz` to use when icon visualization is needed.

💡 **Tip:** Combine with `--git-ignore` to ignore `.gitignore` files when listing.

---

### zoxide

Smart navigation between paths based on usage frequency and recent navigation

**Features**

- 🧠 Learns your most used directories
- ⚡ Jump to any directory with few letters
- 📊 Ranks directories based on access frequency
- 🔍 Integrated fuzzy search

**Installation:**

- **[github.com/ajeetdsouza/zoxide](https://github.com/ajeetdsouza/zoxide)**

**Configuration:**

For Fish:

```bash
# Add to ~/.config/fish/config.fish
zoxide init fish | source
```

**Examples:**

```bash
# After accessing /home/user/projects/my-project multiple times
z my    # Jumps directly to /home/user/projects/my-project

# Interactive search with fzf
zi my   # Opens list of directories that include "my"

# Show history and scores
zoxide query --list
```

⚠️ **Important:** Use the command `z` instead of substituting `cd` (ex: `alias cd="z"`).

💡 **Dica:** Combine with `fzf` for an interactive search using `zi` instead of `z`.

---

### fzf

Interactive Fuzzy finder.

**Features**

- 🔍 Fuzzy search in any list (files, history, processes)
- ⚡ Extremely fast even with millions of entries
- 🎨 Interactive and customizable interface
- 🔌 Shell integration (Ctrl+R for history, Ctrl+T for files)

**Installation:**

- **[github.com/junegunn/fzf](https://github.com/junegunn/fzf)**

**Default Shortcuts after installation:**

- `Ctrl+R` - Search command history
- `Ctrl+T` - Search files and folders
- `Alt+C` - Navigate to a folder

**Suggested configuration:**

Add to your `~/.config/fish/config.fish` (Fish):

```bash
export FZF_CTRL_T_OPTS="
  --walker-skip .git,node_modules,target,.history
  --preview 'bat -n --color=always {}'
  --bind 'ctrl-/:change-preview-window(down|hidden|)'"

export FZF_CTRL_R_OPTS="
  --bind 'ctrl-y:execute-silent(echo -n {2..} | pbcopy)+abort'
  --color header:italic
  --header 'Press CTRL-Y to copy command into clipboard'"

export FZF_ALT_C_OPTS="
  --walker-skip .git,node_modules,target
  --preview 'tree -C {}'"
```

Those configurations improve the experience with the mentioned shortcuts:

- `Ctrl+T`: Ignores common folders (node_modules, .git), shows preview with `bat`, alternates preview with `Ctrl+/`
- `Ctrl+R`: Allows copying a command to clipboard with `Ctrl+Y`
- `Alt+C`: Ignores common folders, shows directory structure with `tree`

💡 **Tip:** Configure `FZF_DEFAULT_OPTS` to configure colors and behavior.

---

## 4. Visual Studio Code

### VSCode Insiders - Suggestion

**Strongly suggest to use [VSCode Insiders](https://code.visualstudio.com/insiders/)** instead of the stable version.

**Why use VSCode Insiders?**

- ✅ Daily updates with latest functionalities
- ✅ Early access to new resources and improvements
- ✅ Surprisingly stable even with the frequent updates
- ✅ Same experience as stable version
- ✅ Does not interfere with stable version (both can be installed)

**⚠️ IMPORTANT about settings.json:**

Some of the current settings **can only work on VSCode Insiders**. When adding a setting on `settings.json` and it appears with a darker color, it means that:

- Setting is not supported on current VSCode version
- Setting can be a experimental functionality only available on Insiders
- Will be supported on future stable VSCode versions

**⚠️ About Insider extensions:**

When using VSCode Insiders, some extensions (specially from Microsoft) can request to switch to **Pre-Release Version** instead of the stable one. Accept those suggestions to ensure total compatibility with Insiders and have access to advanced functionalities that only exist on a pre-release version.

<!-- ### 🌙 Theme -->

<!-- I use [Github Theme](https://marketplace.visualstudio.com/items?itemName=GitHub.github-vscode-theme) no estilo `Github Dark`. -->

### 🔤 Typography (Font-family)

I use [JetBrains Mono](https://www.jetbrains.com/lp/mono/) as default.

Install it on the computer and activate it on VSCode adjusting `editor.fontFamily` option.

```json
"editor.fontFamily": "\"JetBrains Mono\", 'Courier New', monospace",
```

This property allows other fallback fonts if the first one is not found.

### 📦 Suggested extensions

To install the extensions, you should run the following script:

**VSCode Insiders (Suggested):**

```bash
wget https://raw.githubusercontent.com/argentinaluiz/my-vscode-settings/main/vscode-settings/extensions.txt
wget -O - https://raw.githubusercontent.com/argentinaluiz/my-vscode-settings/main/install-extensions-insiders.sh | bash
```

**VSCode:**

```bash
wget https://raw.githubusercontent.com/argentinaluiz/my-vscode-settings/main/vscode-settings/extensions.txt
wget -O - https://raw.githubusercontent.com/argentinaluiz/my-vscode-settings/main/install-extensions.sh | bash
```

**💡 Tip:** `extensions.txt` can be edited to remove unwanted extensions before running the script.

**ℹ️ Note:** Some extensions will be disabled after installation, as they are used only in specific scenarios. They can be enabled on the **extensions** tab.

**📌 Suggestions:** The complete list is on `extensions.txt` file. It has multiple extensions. Below are highlighted the **top or essential suggestions**

#### 🤖 GitHub Copilot - Free AI

[GitHub Copilot Chat](https://marketplace.visualstudio.com/items?itemName=GitHub.copilot-chat) is the main GitHub's AI tool and can be used **for free**.

**⚠️ Note:** GitHub copilot's extension without chat is being deprecated. All its functionalities (autocomplete, chat, code generation) are now integrated in **GitHub Copilot Chat**.

**Features**:

- ✅ Autocomplete code with AI
- ✅ Integrated Chat to answer questions and generate code
- ✅ SReal time contextual suggestions
- ✅ Automatic test generation

#### Code Spell Checker

Essential to avoid code spelling mistakes.

[Code Spell Checker English](https://marketplace.visualstudio.com/items?itemName=streetsidesoftware.code-spell-checker)

[Code Spell Checker Portuguese - Brazilian](https://marketplace.visualstudio.com/items?itemName=streetsidesoftware.code-spell-checker-portuguese-brazilian)

[Code Spell Checker Spanish](https://marketplace.visualstudio.com/items?itemName=streetsidesoftware.code-spell-checker-spanish)

#### 🔧 GitHub Actions and Pull Requests

Essential for working with GitHub

- **[GitHub Actions](https://marketplace.visualstudio.com/items?itemName=github.vscode-github-actions)** - Manage and track GitHub Actions directly on VSCode
- **[GitHub Pull Requests](https://marketplace.visualstudio.com/items?itemName=GitHub.vscode-pull-request-github)** - Create, review and manage Pull Requests without exiting the IDE

#### 🌐 REST Client - Test APIs without exiting VSCode

[REST Client](https://marketplace.visualstudio.com/items?itemName=humao.rest-client) Allows HTTP/REST API testing directly on VSCode, without external tools like Postman or Insomnia.

**Why is it important:**

- ✅ Create versioned `.http` or `.rest` files along with your code
- ✅ Rapidly test endpoints with simple syntax
- ✅ Supports environment variables and chained requests
- ✅ Request history and formatted response (JSON, XML, HTML)
- ✅ Perfect to document project's APIs

**Usage example:**

```http
### Get all users
GET https://api.example.com/users HTTP/1.1
Authorization: Bearer {{token}}

### Create new user
POST https://api.example.com/users HTTP/1.1
Content-Type: application/json

{
  "name": "John Doe",
  "email": "john@example.com"
}
```

Just click on "Send Request" above each request to run it and see the response inline.

#### 🐧 WSL - Windows Subsystem for Linux

The extension [WSL](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-wsl) is **essential** for Windows developers that use Linux via WSL. It allows direct connection between VSCode and Linux environment.

**Why is it important:**

- ✅ Dramatically superior I/O performance (directly accessed files on Linux filesystem)
- ✅ All extensions work on Linux context
- ✅ WSL Installed tools and dependencies are available
- ✅ Integrated terminal executes commands directly on Linux

**⚠️ IMPORTANT:** To take advantage of all benefits, VSCode must be on **"WSL: Ubuntu"** mode (bottom left corner).

#### �🐳 Docker Extension

Strongly advice [Docker DX](https://marketplace.visualstudio.com/items?itemName=docker.docker) installation (directly maintained by Docker) instead of Microsoft's Docker. It offers:

- ✅ More robust autocomplete for Dockerfile and Docker Compose
- ✅ Supports Dockerfile Debug (build debug)
- ✅ More frequent updates and more recent resources
- ✅ Better integration with Docker environment

**📺 Tutorial:** How to use Dockerfile Debug [here](https://youtu.be/7tGdy89_Mqo?si=SPjtT5W60pZVlMgd) (pt_BR)

#### 🐳 Dev Containers

Dev Containers extension allows development inside Docker containers, completely isolating local machine's development environment.

**Benefits:**

- ✅ Consistent development environment inside the entire team
- ✅ Does not need to locally install dependencies (Node, Python, Go, etc.)
- ✅ Projects with different programming language versions without conflicts
- ✅ New developer onboarding in minutes
- ✅ "It works on my machine" stops being a problem

**📺 Complete tutorial:** [Dev Container: Develop applications without installing anything locally](https://youtu.be/kPA9PR7GCrY?si=WF4I85biXFlPTNtW) (pt_BR)

If you use Dev Containers extension to improve your environment with Docker, define some default extensions that will always be inside the containers.

Go to File -> Settings, search `dev.containers.defaultExtensions` or directly add them in `settings.json`:

```json
"dev.containers.defaultExtensions": [
  "dbaeumer.vscode-eslint",
  "donjayamanne.githistory",
  "esbenp.prettier-vscode",
  "humao.rest-client",
  "johnpapa.vscode-peacock",
  "mikestead.dotenv",
  "ms-azuretools.vscode-docker",
  "naumovs.color-highlight",
  "oderwat.indent-rainbow",
  "streetsidesoftware.code-spell-checker",
  "streetsidesoftware.code-spell-checker-portuguese-brazilian",
  "xyz.local-history",
  "eamodio.gitlens",
  "github.copilot",
  "alefragnani.bookmarks",
  "GitHub.copilot-chat",
  "redhat.vscode-yaml"
]
```

This settings grants that all those essential extensions are automatically available in any opened container, without manually reinstalling them. That includes linting tools (ESLint), formatting (Prettier), version control (GitLens, Git History), productivity (Copilot, Bookmarks) and other important utilities.

#### 🎨 Peacock extension - Colors by project

This extension allows colors on VSCode borders, helping a better identification of multiple opened VSCode windows. You can create a color schema by technology and select colors to differentiate opened windows.

Open `File -> Settings -> Peacock`, and select the desired color schema. You can edit `settings.json` to easily add more colors. Example:

```json
"peacock.favoriteColors": [
    {
      "name": "Angular",
      "value": "#a6120d"
    },
    {
      "name": "Angular Red",
      "value": "#dd0531"
    },
    {
      "name": "Apache Kafka",
      "value": "#000000"
    },
    {
      "name": "Azure Blue",
      "value": "#007fff"
    },
    {
      "name": "Docker",
      "value": "#1d63ed"
    },
    {
      "name": "Django",
      "value": "#0C4B33"
    },
    {
      "name": "Golang",
      "value": "#007d9c"
    },
    {
      "name": "JavaScript Yellow",
      "value": "#f9e64f"
    },
    {
      "name": "Java",
      "value": "#f7901e"
    },
    {
      "name": "Keycloak",
      "value": "#4d4d4d"
    },
    {
      "name": "Kubernetes",
      "value": "#436ee3"
    },
    {
      "name": "Laravel",
      "value": "#fb503b"
    },
    {
      "name": "Loopback",
      "value": "#3f5dff"
    },
    {
      "name": "Mandalorian Blue",
      "value": "#1857a4"
    },
    {
      "name": "Nest.js",
      "value": "#e0234e"
    },
    {
      "name": "Node Green",
      "value": "#215732"
    },
    {
      "name": "Python",
      "value": "#25415d"
    },
    {
      "name": "React Blue",
      "value": "#61dafb"
    },
    {
      "name": "Something Different",
      "value": "#832561"
    },
    {
      "name": "Svelte Orange",
      "value": "#ff3d00"
    },
    {
      "name": "Vue Green",
      "value": "#42b883"
    },
    {
      "name": "RabbitMQ",
      "value": "#f60"
    },
    {
      "name": "TypeScript",
      "value": "#007acc"
    }
  ],
```

##### Element adjustments

```json
"peacock.elementAdjustments": {
  "statusBar": "darken",
  "titleBar": "darken",
  "activityBar": "darken"
},
"peacock.affectTabActiveBorder": true
```

This settings slightly darken the status bar, title bar and activity bar to create contrast with the chosen color. Last option also colors active window's border, making it easier to identify it.

---

## ✏️ Editor and productivity

### ⚙️ Editor settings

Settings that improve visual and navigation experience:

#### Font size and spacing

```json
"editor.fontSize": 13.2,
"editor.lineHeight": 1.7
```

Defines font size in 13.2 pixels and line spacing in 1.7, resulting in a better code legibility.

#### Zoom with mouse's wheel

```json
"editor.mouseWheelZoom": true
```

Allows zooming inside the editor by holding `Ctrl` and scrolling mouse's wheel, facilitating fast visualization adjustments.

#### Linked Editing

```json
"editor.linkedEditing": true
```

When activated, editing a HTML/JSX tag, closing tag is automatically updated. Very helpful to avoid syntax errors.

#### Bracket pair colorization

```json
"editor.bracketPairColorization.enabled": true,
"editor.bracketPairColorization.independentColorPoolPerBracketType": true
```

Automatically colors `{}`, `[]` and `()` pairs with different colors, allowing nested code blocks. The second option uses independent colors for every type of bracket.

#### Font ligatures

```json
"editor.fontLigatures": true
```

Activates typography ligatures. If fonts like Fira Code or JetBrains Mono are used and you prefer to see joint characters instead of split ones (like `!=`, `=>`, `>=`), keep as `true`.

### 🔍 Inlay Hints

Inlay Hints are visual hints that appear inline like variable types, function parameters, return values and more. They significantly improve code readability without the need to hover over elements with the mouse.

#### Global settings

```json
"editor.inlayHints.enabled": "offUnlessPressed",
"editor.inlayHints.padding": true
```

- `"offUnlessPressed"`: Hints are hidden by default and appear only when `Ctrl+Alt` is pressed
- `padding`: Adds spacing around hints to improve readability

#### TypeScript and JavaScript

```json
"typescript.inlayHints.parameterNames.enabled": "all",
"typescript.inlayHints.variableTypes.enabled": true,
"typescript.inlayHints.propertyDeclarationTypes.enabled": true,
"typescript.inlayHints.parameterTypes.enabled": true,
"typescript.inlayHints.functionLikeReturnTypes.enabled": true,
"typescript.inlayHints.enumMemberValues.enabled": true,

"javascript.inlayHints.parameterNames.enabled": "all",
"javascript.inlayHints.propertyDeclarationTypes.enabled": true,
"javascript.inlayHints.variableTypes.enabled": true,
"javascript.inlayHints.parameterTypes.enabled": true,
"javascript.inlayHints.functionLikeReturnTypes.enabled": true,
"javascript.inlayHints.enumMemberValues.enabled": true
```

Displays inline:

- **Parameter names**: Displays the name of the parameter next to the assigned value when calling a function
- **Variable types**: Displays the inferred variable type
- **Property types**: Displays typing in property declarations in classes and interfaces
- **parameter types**: Displays types of function parameters
- **Return types**: Displays return types on functions
- **Enum values**: Displays enum numeric values

### ⚡ Productivity settings

Settings that improve development efficiency:

#### Inline suggestions

```json
"editor.inlineSuggest.enabled": true
```

Allows GitHub Copilot's suggestions and other AI extensions directly in the editor while typing.

#### File Nesting

```json
"explorer.fileNesting.enabled": true
```

Groups related files inside the explorer. By default, VSCode already groups files like `.ts` and its `.js`, `package.json` and `package-lock.json`, etc. Those rules can be customized at `explorer.fileNesting.patterns`.

#### Quick Suggestions

```json
"editor.quickSuggestions": {
  "other": "on",
  "comments": "on",
  "strings": "on"
}
```

Activates automatic code suggestions in all contexts: normal code, comments and inside strings. Significantly improves productivity with autocomplete.

#### Import Module Specifier (TypeScript)

```json
"typescript.preferences.importModuleSpecifier": "project-relative"
```

When automatically adding imports, uses project relative paths instead of current file's path. Helps refactoring and consistent imports.

#### Automatic import updates

```json
"javascript.updateImportsOnFileMove.enabled": "always"
```

Allows automatic import updates when moving files. Defined as `"never"` to have manual control, and `"always"` for automatic updates.

### 💻 Terminal settings

#### Copy text on selection

```json
"terminal.integrated.copyOnSelection": true
```

Automatically copies to clipboard any integrated terminal's selected text.

---

## 🤖 AI and advanced tools

### 🚀 GitHub Copilot Chat

The following settings optimize GitHub's chat experience:

#### Autocompletions

```json
"github.copilot.editor.enableAutoCompletions": true
```

Allows automatic code suggestions while typing. Essential to take maximum advantage of **GitHub Copilot** extension.

#### Activation control by filetype

```json
"github.copilot.enable": {
  "*": true,
  "plaintext": false,
  "markdown": true
}
```

Defines in which filetypes is Copilot active.

#### Next Edit Suggestions

```json
"github.copilot.nextEditSuggestions.enabled": true
```

Allows Copilot's suggestions for the next probable suggestions, anticipating your needs.

#### Code Lens for test generation

```json
"github.copilot.chat.generateTests.codeLens": true
```

Adds a "Generate Tests" button above classes and functions, allowing automatic test generation with Copilot's Chat.

#### Inline Chat

```json
"github.copilot.chat.inlineChatCompletionTrigger.enabled": true,
"inlineChat.enableV2": true,
"terminal.integrated.experimentalInlineChat": true
```

Enables Copilot's chat inline directly in the editor, allowing questions and code editing without opening the sidebar. The last option activates inline chat on the integrated terminal.

#### Temporal Context

```json
"github.copilot.chat.editor.temporalContext.enabled": true,
"github.copilot.chat.edits.temporalContext.enabled": true
```

Allows Copilot to use a editing history to give more relevant context-based suggestions based on current workflow.

#### Code Search

```json
"github.copilot.chat.codesearch.enabled": true,
"github.copilot.chat.newWorkspace.useContext7": true
```

Allows Copilot Chat code search and uses Context7 system to improve workspace's context understanding.

#### Language Context

```json
"github.copilot.chat.languageContext.inline.typescript.enabled": true,
"github.copilot.chat.languageContext.fix.typescript.enabled": true,
"github.copilot.chat.languageContext.typescript.enabled": true
```

Gives TypeScript specific context to Copilot's Chat, improving suggestions for editions and adjustments.

#### Chat settings

```json
"chat.editing.alwaysSaveWithGeneratedChanges": true,
"chat.detectParticipant.enabled": true,
"chat.editRequests": "hover",
"chat.edits2.enabled": true
```

- **alwaysSaveWithGeneratedChanges**: Automatically saves files after Copilot is done making adjustments.
- **detectParticipant**: Automatically detects which chat agent to use (@workspace, @vscode, etc.)
- **editRequests**: Shows edition buttons on mouse hover
- **edits2**: Enables Copilot's Chat new interface

### 📝 Code Spell Checker

Helps avoiding typing mistakes in code, comments and strings.

#### Supported languages

```json
"cSpell.language": "en,pt,pt_BR,es_MX"
```

Activates orthographical verification in the desired languages. To use, install **Code Spell Checker** and other desired languages extensions like **Code Spell Checker Portuguese - Brazilian**.

#### Custom dictionary

```json
"cSpell.userWords": [
  "nestjs",
  "typeorm",
  "kubernetes",
  "postgresql",
  "rabbitmq",
  "dockerize",
  "microservices",
  ...
]
```

Adds technical words, framework names, libraries, project names and specific terms to avoid them being marked as mistakes.

---

## 💾 Backup e Synchronization

Since 2022, VSCode allows setting backup and GitHub's server synchronization.

**🔗 How to activate:** Follow instructions at: [https://code.visualstudio.com/docs/editor/settings-sync](https://code.visualstudio.com/docs/editor/settings-sync)

**Benefits:**

- ✅ Never lose your settings again
- ✅ Automatically synchronize between multiple computers
- ✅ Keep extensions, keybindings and snippets always updated

---

## 5. PowerToys

Free Microsoft tools to improve productivity.

### Essential tools

**PowerToys Run** (`Alt + Space`)

- Fast launcher like Spotlight/Alfred for Windows
- Instant file and app search, command execution
- Integrated calculator, unit converter and system plugin
- Replaces Windows' native search with much more speed

**FancyZones**

- Create custom window layouts to organize your workspace
- Drag windows to pre-defined zones (editor + terminal + browser)
- Essential for people with multiple screens
- Save different layouts for different projects

**Color Picker** (`Win + Shift + C`)

- Capture any screen's color with pixel precision
- Available formats: HEX, RGB, HSL, CMYK
- Color history to reuse
- Perfect for design, UI debugging and web development

**PowerRename**

- Rename multiple files with search and replace
- Complete support for regular expressions (regex)
- Realtime preview before applying changes
- Useful for organizing assets, exports renaming, clean filenames

**Other tools:**

- **Always on Top** (`Win + Ctrl + T`) - Fix important windows while working in others
- **Text Extractor** (`Win + Shift + T`) - Optical character recognition to copy text from images and PDFs
- **Keyboard Manager** - Map keys or custom shortcuts
- **Image Resizer** - Resize multiple images directly on file explorer
- There are many other PowerToys tools that are worth exploring

### Installation

**Microsoft Store**

- Search "PowerToys" in Microsoft Store
- Click in "Install"
- Automatic updates

**Documentation:** [learn.microsoft.com/windows/powertoys](https://learn.microsoft.com/pt-br/windows/powertoys/)

---

[← Back to main Readme](../README.md)
