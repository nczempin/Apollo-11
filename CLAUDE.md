# CLAUDE.md - AI Assistant Guide for Apollo-11 Repository

## Repository Overview

This repository contains the original **Apollo 11 Guidance Computer (AGC) source code** for both the Command Module (Comanche055) and Lunar Module (Luminary099). This is a **historical archive** - the code has been digitized from paper printouts and represents the actual software that guided humanity's first moon landing in 1969.

### Critical Context

**This is NOT a typical software project.** The primary goal is historical preservation and accuracy, not feature development or code improvement. Every character, every typo, every spacing decision must match the original 1969 paper scans exactly.

### Repository Stats

- **Language**: AGC Assembly Language (Apollo Guidance Computer Assembly)
- **License**: Public domain
- **Structure**:
  - `Comanche055/` - Command Module (CM) AGC code (85 files)
  - `Luminary099/` - Lunar Module (LM) AGC code (90 files)
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
├── README.md              # Main documentation (+ 27 translations)
├── CONTRIBUTING.md        # Contribution guidelines (+ 18 translations)
├── .editorconfig          # Editor configuration
├── .mdlrc                 # Markdown lint rules
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
- **markdownlint**: Validates all `.md` files
- **Auto-labeling**: Applies labels based on file changes

### Markdown Linting

Configuration in `.mdlrc` disables certain rules:
```ruby
rules '~MD007', '~MD010', '~MD013', '~MD026', '~MD033', '~MD036'
```

These exceptions accommodate the unique formatting needs of this historical documentation.

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

The repository supports 27+ languages:
- README files: `README.[lang].md` (e.g., `README.de.md`, `README.ja.md`)
- CONTRIBUTING files: `CONTRIBUTING.[lang].md`

### Language Codes

- `de` - German (Deutsch)
- `ja` - Japanese (日本語)
- `zh_cn` - Simplified Chinese
- `zh_tw` - Traditional Chinese
- `ko_kr` - Korean
- `es` - Spanish
- `fr` - French
- `pt_br` - Brazilian Portuguese
- And many more...

### Adding Translations

When adding translations:
1. Use the correct language code
2. Follow the existing README/CONTRIBUTING structure
3. Update the language list in the main README.md
4. Title your PR: `Add [Language] [README|CONTRIBUTING]`

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

1. Open the scan images for the relevant pages
2. Open the .agc file in the repository
3. Compare line-by-line, character-by-character
4. Note any discrepancies
5. Verify discrepancies against scans
6. Make corrections that bring code closer to scans
7. Create PR with title: `Proof [FILENAME] #[ISSUE]`

### Adding a Translation

1. Copy README.md or CONTRIBUTING.md
2. Rename to README.[lang].md or CONTRIBUTING.[lang].md
3. Translate all content (maintaining structure and formatting)
4. Add language to the list in main README.md
5. Create PR with title: `Add [Language] README` or `Add [Language] CONTRIBUTING`

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

## Conclusion

This repository is a window into computing history - the software that guided Apollo 11 to the moon. Every contribution helps preserve this legacy accurately for future generations. Approach all changes with care, precision, and respect for the original work.

When in doubt, check the scans. When still in doubt, ask the maintainers.

---

*Last updated: 2025-11-17*
*This file is intended for AI assistants working with the Apollo-11 repository*
