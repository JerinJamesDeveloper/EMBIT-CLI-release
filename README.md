# ⚡ Embit CLI

> 🚀 **Accelerate Flutter development using Clean Architecture** inside projects built with the **Embit starter-kit ecosystem**.

Embit acts as a **code generator and architecture assistant**, helping developers create structured features, usecases, models, repositories, and BLoC scaffolding — automatically.

Instead of manually writing dozens of boilerplate files, `embit` generates the required architecture in **seconds**, keeping your project consistent with **Embit architecture conventions**.

---

## 🎯 Perfect For

| Use Case | Description |
|----------|-------------|
| 📱 **Scalable Flutter Apps** | Grow without losing structure |
| 👥 **Large Teams** | Consistent architecture across contributors |
| 🏃 **Rapid MVP Development** | Go from idea to feature in seconds |
| 🏢 **Enterprise Projects** | Strict separation of concerns, enforced |

---

## 🧩 Overview

Modern Flutter projects following **Clean Architecture** demand significant boilerplate for every new feature. Typically, creating one feature involves writing:

- 🗂️ Entities & Models
- 🔌 Repositories & Data Sources
- 🧠 Usecases
- 🔄 BLoC State Management
- 🖥️ UI Pages & Widgets

> ⏱️ This setup can take **20–40 minutes per feature**, even for experienced developers.

### ✅ Embit fixes that.

With a single command:

```bash
embit feature -n orders -u get_orders -t get-list
```

Embit generates the **complete feature structure** — all files, all layers, correctly wired. 🎉

---

## 🏗️ What Embit CLI Generates

| Layer | Description |
|-------|-------------|
| 📦 **Feature** | Root module for a specific app capability |
| 🧱 **Model / Entity** | Data structures representing business data |
| 🔀 **Repository** | Abstraction layer between domain and data |
| 🌐 **Datasource** | API, local DB, or external service access |
| 🧠 **Usecase** | Business logic operations |
| 🔄 **BLoC** | State management logic |
| 🖥️ **Page** | UI screen for the feature |
| 🧩 **Widgets** | Reusable UI components |

### 📁 Clean Architecture Folder Structure

```
📂 presentation
  ├── 🔄 bloc
  ├── 🖥️ pages
  └── 🧩 widgets

📂 domain
  ├── 🧱 entities
  ├── 🔀 repositories
  └── 🧠 usecases

📂 data
  ├── 📦 models
  ├── 🌐 datasources
  └── 🔀 repositories
```

---

## 💡 Why Use Embit CLI?

### ⚡ Faster Development
Generate a full feature scaffold in **seconds** instead of manually writing boilerplate.

### 🎯 Consistent Architecture
All generated code follows the **same folder structure and conventions** across the project.

### 📈 Scalable Projects
Large projects stay maintainable because features follow **predictable patterns**.

### 🛡️ Reduced Human Error
Automatically generates correct file names, imports, and architecture wiring — no typos, no missing files.

### 🤝 Better Team Collaboration
Every team member follows the **same development workflow**, reducing onboarding time and confusion.

---

## 📚 Table of Contents

- [⚙️ Installation](#️-installation)
- [📋 Supported Commands](#-supported-commands)
- [📥 Clone Command](#-clone-command)
- [✨ Feature Command](#-feature-command)
- [🧠 Usecase Command](#-usecase-command)
- [🧱 Model Command](#-model-command)
- [🗺️ Recommended Workflow](#️-recommended-workflow)
- [🔄 Update Command](#-update-command)
- [📝 Notes](#-notes)

---

## ⚙️ Installation

### 📁 Local Path Install

```bash
dart pub global activate --source path .
```

### 🌐 Git Install

```bash
dart pub global activate --source git <your_repo_url>
```

### ✅ Verify Installation

```bash
embit --version
```

---

## 📋 Supported Commands

```bash
embit clone <path_to_kit_folder>
embit feature --name <feature_name> [options]
embit usecase --feature <feature_name> --name <usecase_name> [options]
embit model --feature <feature_name> --name <model_name> [options]
embit update
```

---

## 📥 Clone Command

Copy a licensed kit into your current project root.

```bash
embit clone <path_to_kit_folder>
```

**Example:**

```bash
embit clone C:\starter_kits\nexus
```

**Behavior:**

- 📋 Copies the full kit into the current working directory
- ♻️ Overwrites existing files when the same path already exists
- 🔑 Reads `LICENSE_KEY` from the kit's `.embit` file
- 💾 Stores the license key permanently outside the project
- 🚫 Skips copying the `.embit` file into the destination project

---

## ✨ Feature Command

The `feature` command creates a complete feature scaffold in one shot:

- ✅ One feature folder
- ✅ One main model/entity
- ✅ One primary usecase
- ✅ Repository scaffold
- ✅ Datasource scaffold
- ✅ BLoC scaffold
- ✅ Page scaffold
- ✅ Widget scaffold

```bash
embit feature -n <feature_name> -m <model_name> -u <usecase_name> -t <type>
```

### ⚙️ Options

| Flag | Description |
|------|-------------|
| `-n`, `--name` | Feature name in `snake_case` |
| `-m`, `--model` | Primary model name (defaults to singular feature name) |
| `-u`, `--usecase` | Primary usecase name |
| `-t`, `--type` | `get`, `get-list`, `create`, `update`, `delete`, or `custom` |
| `--string` | Add a `String` model field |
| `--int` | Add an `int` model field |
| `--double` | Add a `double` model field |
| `--bool` | Add a `bool` model field |
| `--datetime` | Add a `DateTime` model field |
| `--with-example` | Include example implementation |
| `--nav-bar` | Add feature to bottom navigation |
| `--icon` | Navigation icon |
| `--label` | Navigation label |
| `-f`, `--force` | Overwrite if the feature already exists |
| `--dry-run` | Preview without writing files |
| `-i`, `--interactive` | Prompt for navigation options |

> 💡 **Default model fields** when none are provided: `id: String`, `title: String`, `createdAt: DateTime`, `updatedAt: DateTime?`

### 📌 Examples

```bash
# 🛒 Orders feature with custom fields
embit feature -n orders -m order -u get_orders -t get-list ^
  --string id ^
  --string orderNumber ^
  --double totalAmount ^
  --string "status?" ^
  --datetime createdAt
```

```bash
# 💳 Checkout session with custom type
embit feature -n checkout -m checkout_session -u start_checkout -t custom ^
  --string id ^
  --double amount ^
  --string currency ^
  --bool "isGuest=false"
```

```bash
# 📦 Minimal product feature using defaults
embit feature -n products
```

---

## 🧠 Usecase Command

Add more business actions to an existing feature.

```bash
embit usecase -f <feature> -n <usecase_name> -t <type> [params]
```

### ⚙️ Options

| Flag | Description |
|------|-------------|
| `-f`, `--feature` | Existing feature name |
| `-n`, `--name` | Usecase name in `snake_case` |
| `-t`, `--type` | `get`, `get-list`, `create`, `update`, `delete`, or `custom` |
| `--with-event` | Generate BLoC event wiring |
| `--force` | Overwrite if usecase already exists |
| `--dry-run` | Preview generated changes |
| `-i`, `--interactive` | Guided prompts |
| `--string`, `--int`, `--double`, `--bool`, `--datetime` | Parameter fields |

### 📌 Examples

```bash
# 📦 Archive an order
embit usecase -f orders -n archive_order -t update --with-event
```

```bash
# 📰 Get trending posts in a feed
embit usecase -f feed -n get_trending_posts -t get-list
```

```bash
# 🎟️ Apply coupon at checkout
embit usecase -f checkout -n apply_coupon -t custom ^
  --string code ^
  --string "orderId?" ^
  --with-event
```

---

## 🧱 Model Command

Add more entities and models after a feature has been created.

```bash
embit model -f <feature> -n <model_name> [field options]
```

### ⚙️ Options

| Flag | Description |
|------|-------------|
| `-f`, `--feature` | Feature name |
| `-n`, `--name` | Model name |
| `--string`, `--int`, `--double`, `--bool`, `--datetime` | Typed fields |
| `--custom` | Custom field definition e.g. `Care` or `items:List<Item>` |
| `-s`, `--source` | Generate a local data source |
| `--with-state` | Generate BLoC state additions for the model |

### 📌 Examples

```bash
# 🧾 Order item model
embit model -f orders -n OrderItem ^
  --string id ^
  --string sku ^
  --int quantity ^
  --double unitPrice
```

```bash
# 🛍️ Product model with custom fields
embit model -f products -n Product ^
  --string id ^
  --string name ^
  --custom Care ^
  --custom "items:List<ItemEntity>" ^
  --with-state
```

---

## 🗺️ Recommended Workflow

```
1️⃣  Clone or open a starter-kit project
        ↓
2️⃣  Create your first feature with  embit feature
        ↓
3️⃣  Add more models later with  embit model
        ↓
4️⃣  Add more business actions with  embit usecase
```

---

## 🔄 Update Command

Keep Embit CLI up to date with the latest version.

```bash
embit update
```

This command checks for a newer version and installs it automatically. ✅

---

## 📝 Notes

> ⚠️ The following commands are **not** part of the current CLI:
> `embit init`, `embit generate`, `embit build`, `embit clean`

💬 Run `embit <command> --help` for command-specific help at any time.

---

<div align="center">

**Built with ❤️ for Flutter developers who value clean, scalable architecture.**

</div>
