# CLAUDE.md - AI Assistant Guide for Apollo-11 Repository

## Repository Overview

This repository contains the original **Apollo 11 Guidance Computer (AGC) source code** for both the Command Module (Comanche055) and Lunar Module (Luminary099). This is a **historical archive** - the code has been digitized from paper printouts and represents the actual software that guided humanity's first moon landing in 1969.

### Critical Context

**This is NOT a typical software project.** The primary goal is historical preservation and accuracy, not feature development or code improvement. Every character, every typo, every spacing decision must match the original 1969 paper scans exactly.

### Repository Stats

- **Language**: AGC Assembly Language (Apollo Guidance Computer Assembly)
- **License**: Public domain
- **Supported Languages**: 30+ translations in multiple languages
- **Structure**:
  - `Comanche055/` - Command Module (CM) AGC code (85 files)
  - `Luminary099/` - Lunar Module (LM) AGC code (90 files)
  - `Translations/` - README and CONTRIBUTING files in 30+ languages
- **Historical Significance**: Led by Margaret H. Hamilton, this code represents pioneering work in software engineering

## Codebase Structure

```
Apollo-11/
├── Comanche055/           # Command Module AGC source (Colossus 2A)
│   ├── CONTRACT_AND_APPROVALS.agc
│   ├── ALARM_AND_ABORT.agc
│   ├── EXECUTIVE.agc
│   ├── DISPLAY_INTERFACE_ROUTINES.agc
│   └── ... (85 .agc files total)
├── Luminary099/           # Lunar Module AGC source (Luminary 1A)
│   ├── BURN_BABY_BURN--MASTER_IGNITION_ROUTINE.agc
│   ├── AGC_BLOCK_TWO_SELF_CHECK.agc
│   ├── ASCENT_GUIDANCE.agc
│   └── ... (90 .agc files total)
├── Translations/          # Internationalization
│   ├── README.*.md        # README translations (30+ languages)
│   └── CONTRIBUTING.*.md  # CONTRIBUTING translations (30+ languages)
├── README.md              # Main documentation
├── CONTRIBUTING.md        # Contribution guidelines
├── .editorconfig          # Editor configuration
├── .markdownlint.yml      # Markdown lint configuration
└── .github/
    ├── workflows/
    │   ├── markdownlint.yml  # CI for markdown linting
    │   └── label.yml         # Auto-labeling
    └── ISSUE_TEMPLATE/       # Issue templates for proofing

```

### File Naming Conventions

AGC files use uppercase with underscores:
- `ALARM_AND_ABORT.agc`
- `DISPLAY_INTERFACE_ROUTINES.agc`
- `BURN_BABY_BURN--MASTER_IGNITION_ROUTINE.agc` (note: double dash for "BURN, BABY, BURN")

## AGC Assembly Language Basics

### File Structure

Every `.agc` file follows this format:

```agc
# Copyright:    Public domain.
# Filename:     [FILENAME].agc
# Purpose:      Part of the source code for Colossus 2A / Luminary 1A
# Assembler:    yaYUL
# Contact:      Ron Burkey <info@sandroid.org>
# Website:      www.ibiblio.org/apollo
# Mod history:  [Date] [Initials] [Description]

# Page [number]

# Comments and actual AGC assembly code
[CODE]
```

### Key Elements

- **Comments**: Start with `#` and must match scans exactly
- **Line markers**: `R0000` format in column 1 (e.g., `R0819`)
- **Instructions**: AGC assembly mnemonics (e.g., `CS`, `TC`, `TCF`)
- **Labels**: Used for jumps and references
- **Page markers**: `# Page [number]` indicate page boundaries from original scans

### Formatting Rules (CRITICAL)

These rules are **mandatory** and enforced by `.editorconfig`:

#### For `.agc` files:
- **Indentation**: TABS ONLY (no spaces)
- **Tab width**: 8 characters
- **Encoding**: UTF-8
- **Line endings**: LF (Unix-style)
- **Trailing whitespace**: Must be trimmed
- **Final newline**: Required

#### For `.md` files:
- **Indentation**: 2 spaces
- **Encoding**: UTF-8
- **Line endings**: LF
- **Trailing whitespace**: Must be trimmed

## Development Workflow

### What Changes Are Accepted?

**ONLY** the following types of changes:

1. **Proofing corrections**: Fixing discrepancies between digitized code and original scans
2. **Translation additions**: Adding new README/CONTRIBUTING translations
3. **Documentation updates**: Clarifying contribution guidelines
4. **CI/tooling improvements**: GitHub Actions, linting rules

**NEVER ACCEPTED**:
- Code refactoring or modernization
- Performance improvements
- Adding new features
- Changing logic or algorithms
- "Fixing" typos that exist in original scans

### The Golden Rule: Match the Scans

Every change must make the digitized code more accurate to these sources:
- **Comanche055**: http://www.ibiblio.org/apollo/ScansForConversion/Comanche055/
- **Luminary099**: http://www.ibiblio.org/apollo/ScansForConversion/Luminary099/
- **Navigation Tool**: https://28gpc.csb.app/ - Interactive website to easily navigate the scanned printouts

### Proofing Process

When proofing AGC files:

1. **Compare against scans**: Open the scan images and compare character-by-character
2. **Check comments**: Comments must match EXACTLY, including:
   - Typos (if in original, keep them; if not in original, remove them)
   - Spacing (see spacing rules below)
   - Capitalization
   - Punctuation
3. **Check code**: Verify instructions, labels, and operands
4. **Check formatting**: Tab alignment, line breaks

#### Comment Spacing Rules

- **Single space**: Between words
- **Double space**: Between sentences
- **Triple space**: For indentations

Example from scans should be followed exactly.

#### Line Break Rules

- **With R0000 markers**: Must match scans exactly
- **Without R0000 markers**: Only 1-2 blank lines allowed
  - Strip extra blank lines (unless they have R0000 markers)
  - These were created by unprinted digits in column 8 of punch cards
  - 2 = double space (one blank line)
  - 3 = triple space (two blank lines)

### Creating Pull Requests

#### PR Titles Must Follow Format:

**For proofing work**:
```
Proof [FILE NAME] #[PROOF ISSUE]
```
Example: `Proof ALARM_AND_ABORT #564`

**For translations**:
```
Add [LANGUAGE] [README|CONTRIBUTING]
```
Example: `Add Dutch README`

#### PR Best Practices

- **Small PRs**: Focus on a few pages at a time
- **Reference pages**: Mention which pages you checked (e.g., "Pages 45-52")
- **Link to scans**: Reference specific scan pages if helpful
- **One file at a time**: Easier to review

### Issue Templates

The repository provides templates for:
- `Proof_Comanche.md` - For Command Module proofing
- `Proof_Luminary.md` - For Lunar Module proofing
- `Discussion.md` - For general discussions
- `Humour.md` - For fun historical anecdotes

## Code Quality & CI

### Continuous Integration

The repository runs:
- **markdownlint**: Validates all `.md` files using `markdownlint-cli2`
- **Auto-labeling**: Applies labels based on file changes

### Markdown Linting

The repository uses **markdownlint-cli2** (via GitHub Actions) with configuration in `.markdownlint.yml`.

Disabled rules to accommodate historical documentation formatting:
- `MD007` - Unordered list indentation
- `MD010` - Hard tabs
- `MD013` - Line length
- `MD026` - Trailing punctuation in heading
- `MD033` - Inline HTML
- `MD034` - Bare URL
- `MD036` - Emphasis used instead of heading
- `MD041` - First line in file should be top-level heading
- `MD050` - Strong style
- `MD053` - Link reference definition

These exceptions accommodate the unique formatting needs of this historical documentation and multi-language support.

## Editor Support

### Recommended Extensions

AGC Assembly syntax highlighting is available for:
- **Atom** (with auto-formatting)
- **Sublime Text 3** (with auto-formatting)
- **Visual Studio Code** (with auto-formatting) - https://github.com/wopian/agc-assembly
- **Vim** - https://github.com/wsdjeg/vim-assembly
- **Eclipse**
- **Kate**
- And others (see CONTRIBUTING.md)

### EditorConfig

Most modern editors support `.editorconfig` automatically. This ensures:
- Correct indentation (tabs for .agc, spaces for .md)
- Proper line endings
- Trimmed whitespace

## Working with Translations

### Translation Files

The repository supports **30+ languages** with translations stored in the `Translations/` directory:
- README files: `Translations/README.[lang].md`
- CONTRIBUTING files: `Translations/CONTRIBUTING.[lang].md`
- Main files remain at root: `README.md`, `CONTRIBUTING.md` (English)

### Supported Languages

The repository includes translations in:

**European Languages:**
- `be` - Belarusian (Беларуская мова)
- `ca` - Catalan (Català)
- `cz` - Czech (Čeština)
- `da` - Danish (Dansk)
- `de` - German (Deutsch)
- `es` - Spanish (Español)
- `fi` - Finnish (Suomi)
- `fr` - French (Français)
- `gl` - Galician (Galego)
- `gr` - Greek (Ελληνικά)
- `it` - Italian (Italiano)
- `lt` - Lithuanian (Lietuvių)
- `nl` - Dutch (Nederlands)
- `no` - Norwegian (Norsk)
- `pl` - Polish (Polski)
- `pt_br` - Brazilian Portuguese (Português)
- `ro` - Romanian (Română)
- `ru` - Russian (Русский)
- `sv` - Swedish (Svenska)
- `tr` - Turkish (Türkçe)
- `uk` - Ukrainian (Українська)

**Asian Languages:**
- `ar` - Arabic (العربية)
- `as_in` - Assamese (অসমীয়া)
- `az` - Azerbaijani
- `bd_bn` - Bengali (বাংলা)
- `fa` - Persian/Farsi (فارسی)
- `hi_in` - Hindi (हिंदी)
- `id` - Indonesian (bahasa Indonesia)
- `ja` - Japanese (日本語)
- `jv` - Javanese (Basa Jawa)
- `ko_kr` - Korean (한국어)
- `ku` - Kurdish (Kurdî)
- `ml` - Malayalam (മലയാളം)
- `mm` - Burmese (မြန်မာ)
- `mn` - Mongolian
- `ne` - Nepali (नेपाली भाषा)
- `vi` - Vietnamese (tiếng Việt)
- `zh_cn` - Simplified Chinese (简体中文)
- `zh_tw` - Traditional Chinese (正體中文)

### Adding Translations

When adding translations:
1. Create file in `Translations/` directory: `Translations/README.[lang].md` or `Translations/CONTRIBUTING.[lang].md`
2. Use the correct language code from the list above
3. Follow the existing README/CONTRIBUTING structure exactly
4. Maintain all formatting and markdown structure
5. Update the language list in the main `README.md` and `CONTRIBUTING.md` with proper links
6. Title your PR: `Add [Language] README` or `Add [Language] CONTRIBUTING`
7. Ensure the language name is correctly localized (e.g., "Español" not "Spanish")

## Historical Context

### Key People

- **Margaret H. Hamilton**: Colossus Programming Leader, Apollo Guidance and Navigation
- **Ron Burkey**: Led the digitization effort through Virtual AGC project
- **Paul Fjeld**: Performed the digitization
- **Deborah Douglas**: MIT Museum, arranged digitization

### Assembly Information

**Comanche055** (Command Module):
- Program: Colossus 2A
- Assembly revision: 055
- Date: April 1, 1969
- Build ID: 2021113-051, 10:28 APR. 1, 1969

**Luminary099** (Lunar Module):
- Program: Luminary 1A (LMY99)
- Assembly revision: 001
- Date: July 14, 1969
- Build ID: 2021112-061, 16:27 JUL. 14, 1969

### Notable File Names

Some files have interesting historical names:
- `BURN_BABY_BURN--MASTER_IGNITION_ROUTINE.agc` - Named after DJ Magnificent Montague's catchphrase from the 1960s
- Named by Don Eyles and Peter Adler

## For AI Assistants: Key Principles

### 1. PRESERVATION OVER PERFECTION

Your role is to help preserve historical artifacts, not improve them. Resist the urge to:
- Fix apparent bugs or inefficiencies
- Modernize syntax
- Add explanatory comments
- Reorganize code structure

### 2. ACCURACY IS EVERYTHING

When proofing:
- Compare character-by-character against scans
- Don't assume anything is correct or incorrect
- Check both code and comments with equal care
- Preserve historical typos (e.g., "SPAECRAFT" instead of "SPACECRAFT")

### 3. UNDERSTAND THE CONTEXT

This code:
- Ran on a 16-bit computer with 2KB of RAM
- Was written in the 1960s
- Landed humans on the moon
- Represents groundbreaking software engineering

Treat it with appropriate respect and historical awareness.

### 4. SMALL, FOCUSED CHANGES

When helping with contributions:
- Suggest small PRs (few pages at a time)
- Focus on one file per PR
- Provide clear references to scan pages
- Make it easy for maintainers to verify

### 5. NEVER GUESS

If you're unsure about:
- Whether something matches the scans
- Spacing or formatting details
- Translation accuracy

Always recommend the user check the original scans or ask maintainers.

### 6. RESPECT THE WORKFLOW

- PRs must follow naming conventions
- Changes must reference original scans
- Markdown files must pass linting
- All formatting must follow .editorconfig

## Common Tasks

### Proofing a File

1. Open the scan images for the relevant pages (use https://28gpc.csb.app/ for easy navigation)
2. Open the .agc file in the repository
3. Compare line-by-line, character-by-character
4. Note any discrepancies
5. Verify discrepancies against scans
6. Make corrections that bring code closer to scans
7. Create PR with title: `Proof [FILENAME] #[ISSUE]`

### Adding a Translation

1. Copy README.md or CONTRIBUTING.md
2. Save as `Translations/README.[lang].md` or `Translations/CONTRIBUTING.[lang].md`
3. Translate all content (maintaining structure and formatting)
4. Add language entry to the 🌐 list in main README.md and/or CONTRIBUTING.md
5. Add proper link reference: `[LANG]:Translations/README.[lang].md`
6. Use localized language name (e.g., "Español" not "Spanish")
7. Create PR with title: `Add [Language] README` or `Add [Language] CONTRIBUTING`

### Verifying Formatting

Run editorconfig-compliant editor or check:
```bash
# For .agc files - should show tabs
cat -A filename.agc | head

# Should see ^I for tabs, $ for line endings
```

## Compilation

To actually compile and run this code:
- Visit **Virtual AGC**: https://github.com/rburkey2005/virtualagc
- Uses `yaYUL` assembler
- Can run in AGC simulator

**Note**: AI assistants should NOT attempt to compile or execute this code without explicit user request and proper setup.

## Resources

### Official Links

- **Virtual AGC Project**: http://www.ibiblio.org/apollo/
- **MIT Museum**: http://web.mit.edu/museum/
- **Scan Images (Comanche055)**: http://www.ibiblio.org/apollo/ScansForConversion/Comanche055/
- **Scan Images (Luminary099)**: http://www.ibiblio.org/apollo/ScansForConversion/Luminary099/
- **Interactive Scan Navigator**: https://28gpc.csb.app/ - Easy navigation tool for browsing scans
- **Software Heritage Archive**: https://archive.softwareheritage.org/browse/origin/https://github.com/chrislgarry/Apollo-11/

### GitHub Resources

- **Milestones**: Track proofing progress for Comanche and Luminary
- **Issues**: Proofing tasks for specific files
- **Pull Requests**: Follow strict formatting requirements

## Frequently Asked Questions

### Can I improve the code?

No. The goal is accuracy to the original, not improvement.

### What if I find a bug?

If it exists in the original scans, it stays. This is historical preservation.

### What if the scan is wrong?

Scans are the source of truth. If a scan is illegible, contact Ron Burkey for higher-quality images.

### Can I add documentation?

Only if it helps with the proofing/translation process. Don't add code documentation.

### What language is this?

AGC Assembly Language, specific to the Apollo Guidance Computer.

### Will this code run today?

Yes, using the Virtual AGC simulator and yaYUL assembler.

## Quick Reference for AI Assistants

### File Locations
- AGC source code: `Comanche055/` and `Luminary099/`
- Translations: `Translations/` directory
- Main docs: `README.md`, `CONTRIBUTING.md` (root)
- Editor config: `.editorconfig`
- Lint config: `.markdownlint.yml`

### Key URLs
- Scan navigator: https://28gpc.csb.app/
- Comanche scans: http://www.ibiblio.org/apollo/ScansForConversion/Comanche055/
- Luminary scans: http://www.ibiblio.org/apollo/ScansForConversion/Luminary099/
- Virtual AGC: https://github.com/rburkey2005/virtualagc

### Rules to Remember
1. ✅ Match scans exactly - typos and all
2. ✅ Use tabs (width 8) for .agc files
3. ✅ Small PRs focused on specific pages
4. ✅ Follow PR title format: "Proof [FILE] #[ISSUE]"
5. ❌ Don't fix "bugs" in original code
6. ❌ Don't modernize or refactor
7. ❌ Don't add features or documentation

---

*Last updated: 2026-03-08*
*This file is intended for AI assistants working with the Apollo-11 repository*
