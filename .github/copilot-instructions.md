# Copilot Instructions for Miryoku ZMK

## Repository Overview

This repository contains the Miryoku implementation for ZMK (Zephyr Mechanical Keyboard) firmware. Miryoku is an ergonomic, minimal, orthogonal, and universal keyboard layout. The repository supports building firmware for many different keyboard hardware configurations both locally and via GitHub Actions workflows.

## Key Components

### 1. Keyboard Keymaps (`/config/*.keymap`)
- Keymap files define keyboard configurations for specific hardware
- Each `.keymap` file corresponds to a supported keyboard model
- Keymaps are composed of:
  - A config file reference
  - A mapping for the physical layout from `/miryoku/mapping/`
  - The Miryoku keymap from `/miryoku/miryoku.dtsi`

### 2. Miryoku Core (`/miryoku/`)
- `miryoku.dtsi` - Main devicetree source for the Miryoku layout
- `miryoku.h` - C header file with layout definitions
- `miryoku_behaviors.dtsi` - Custom ZMK behaviors
- `miryoku_*.dtsi` - Feature-specific devicetree includes (mousekeys, shift functions, etc.)
- `mapping/` - Physical layout mappings organized by key count (30, 34, 36, etc.)

### 3. GitHub Actions Workflows (`/.github/workflows/`)
- `build-inputs.yml` - Interactive workflow with form inputs
- `build-example-*.yml` - Example workflows for specific keyboards
- `test-*.yml` - Testing workflows for validation
- Workflows build firmware without local development environment

## File Types and Conventions

### Devicetree Files (`.dtsi`, `.overlay`)
- ZMK uses devicetree for keyboard configuration
- Use C preprocessor directives (`#define`, `#include`, `#ifdef`)
- Follow existing patterns for includes and macros
- Key bindings use ZMK binding syntax: `<BEHAVIOR PARAMETERS>`

### Keymap Files (`.keymap`)
- Include the appropriate mapping header from `/miryoku/mapping/`
- Reference `miryoku.dtsi` for the core layout
- May include optional `.conf` files for keyboard-specific settings

### Configuration Files (`.conf`)
- Key-value pairs for ZMK configuration options
- Enable/disable features like RGB, displays, mouse keys
- Format: `CONFIG_OPTION=y` or `CONFIG_OPTION=n`

## Coding Guidelines

### When Adding New Keyboard Support
1. Create a `.keymap` file in `/config/` named after the keyboard
2. Include the appropriate mapping from `/miryoku/mapping/[key-count]/`
3. Add optional `.conf` file if special features need configuration
4. Test with the appropriate workflow

### When Modifying Core Miryoku Code
1. Changes to `/miryoku/` affect all keyboards - test thoroughly
2. Maintain backward compatibility when possible
3. Use preprocessor guards for optional features
4. Follow existing naming conventions (e.g., `MIRYOKU_*` for macros)

### When Working with Workflows
1. Preserve the matrix build capability for multiple configurations
2. Maintain the form input structure in `build-inputs.yml`
3. Test changes with `test-*.yml` workflows before deployment
4. Document new options in workflow descriptions

## Build and Test

### Local Building
1. Set up ZMK development environment following [ZMK docs](https://zmk.dev/docs/development/setup)
2. Set `ZMK_CONFIG` environment variable to the absolute path of `/config/` directory
3. Build using ZMK's west build system

### Workflow Building
1. Fork the repository and enable GitHub Actions
2. Use "Build Inputs" workflow for interactive builds
3. Use example workflows as templates for custom configurations
4. Firmware artifacts are available as workflow run artifacts

### Testing
- Test workflows validate configurations for all boards/shields
- Run appropriate test workflow after making changes
- Enable debug mode with `MIRYOKU_DEBUG` secret for troubleshooting

## Important Notes

### Copyright and Attribution
- All files include copyright header: `Copyright 2022-2023 Manna Harbour`
- Maintain attribution when modifying existing files

### Documentation Format
- Primary documentation is in `readme.org` (Emacs Org mode format)
- Use Org mode syntax for links: `[[url][description]]`
- Maintain existing documentation structure

### Features and Options
- Caps word
- Double tap boot
- Global shift functions
- Key emulation combos
- Mouse keys
- Soft off
- Tap delay
- Custom layouts (AZERTY, Colemak, Dvorak, QWERTY, etc.)
- Navigation variants (invertedT, vi)

## Common Tasks

### Adding Support for a New Keyboard
1. Research the keyboard's ZMK board/shield names
2. Determine the key count and physical layout
3. Create `config/[keyboard-name].keymap`
4. Include the appropriate mapping header
5. Add example workflow if needed
6. Test with build workflow

### Modifying Keyboard Behavior
1. Check if change should be in core Miryoku (`/miryoku/`) or keyboard-specific (`/config/`)
2. For core changes, use preprocessor guards for optional features
3. For keyboard-specific changes, modify the `.keymap` or `.conf` file
4. Test affected keyboards

### Troubleshooting Build Issues
1. Check workflow logs for errors
2. Enable debug mode with repository secret
3. Verify devicetree syntax and includes
4. Check for missing configuration options in `.conf` files

## Resources

- [ZMK Documentation](https://zmkfirmware.dev/)
- [Miryoku Main Repository](https://github.com/manna-harbour/miryoku)
- [Miryoku ZMK Quickstart Guide](docs/quickstart)
- [ZMK Devicetree Documentation](https://zmk.dev/docs/development/hardware-integration)
