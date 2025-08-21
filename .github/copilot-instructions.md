# oh-my-chill Theme Repository

oh-my-chill is a pastel-themed configuration for oh-my-posh, a cross-platform prompt theme engine for shells (bash, zsh, PowerShell, etc.).

**ALWAYS reference these instructions first and fallback to search or bash commands only when you encounter unexpected information that does not match the info here.**

## Working Effectively

### Bootstrap and Setup
- Install oh-my-posh binary:
  - `curl -s -L -o /tmp/oh-my-posh https://github.com/JanDeDobbeleer/oh-my-posh/releases/latest/download/posh-linux-amd64`
  - `chmod +x /tmp/oh-my-posh`
  - Download takes ~5 seconds, binary is ~19MB
- Validate JSON configuration:
  - `python3 -m json.tool oh-my-chill.omp.json > /dev/null` -- takes <1 second
  - `jq '.' oh-my-chill.omp.json > /dev/null` -- alternative validation method

### Testing and Validation
- Test theme rendering:
  - `/tmp/oh-my-posh print primary --config oh-my-chill.omp.json` -- takes <1 second
  - Should display: `╭─username@hostname─[/current/path]` and `╰─[git-branch-info]- ⚡`
- Debug theme configuration:
  - `/tmp/oh-my-posh debug --config oh-my-chill.omp.json` -- takes <1 second
  - Shows all segments, timing, and cache information
- Validate theme schema:
  - Theme uses official schema: `https://raw.githubusercontent.com/JanDeDobbeleer/oh-my-posh/main/themes/schema.json`
  - All segments should load without errors

### Making Changes
- ALWAYS validate JSON syntax after editing: `python3 -m json.tool oh-my-chill.omp.json > /dev/null`
- ALWAYS test theme rendering after changes: `/tmp/oh-my-posh print primary --config oh-my-chill.omp.json`
- ALWAYS run debug mode to verify segments work: `/tmp/oh-my-posh debug --config oh-my-chill.omp.json`

## Validation Scenarios

**CRITICAL**: After making any changes to the theme configuration, ALWAYS run through these complete validation scenarios:

### Basic Theme Functionality
1. Validate JSON: `python3 -m json.tool oh-my-chill.omp.json > /dev/null`
2. Test primary prompt: `/tmp/oh-my-posh print primary --config oh-my-chill.omp.json`
3. Verify segments load: `/tmp/oh-my-posh debug --config oh-my-chill.omp.json | grep -E "Session|Path|Git|Status"`
4. Check for errors: `/tmp/oh-my-posh debug --config oh-my-chill.omp.json | grep -i error`

### Git Integration Testing
1. Ensure you're in a git repository with changes: `git status`
2. Test git segment rendering: `/tmp/oh-my-posh print primary --config oh-my-chill.omp.json`
3. Verify git branch and status indicators appear in prompt output
4. Check git segment debug info: `/tmp/oh-my-posh debug --config oh-my-chill.omp.json | grep "Git("`

### Multi-Environment Testing
1. Test in directory with package.json (Node.js detection)
2. Test in directory with pyproject.toml or requirements.txt (Python detection)
3. Verify language-specific segments activate correctly
4. Check segment timing in debug output

## Repository Structure

### Key Files
```
.
├── README.md                     # Basic theme description
├── oh-my-chill.omp.json         # Main theme configuration file
└── .github/
    └── copilot-instructions.md   # This file
```

### Theme Configuration Details
- **Schema**: Uses official oh-my-posh v1 schema
- **Segments**: Session, Path, Git, Language detection (Node, Python, Java, etc.), Status
- **Style**: Pastel colors with Unicode box-drawing characters
- **Layout**: Two-line prompt with right-aligned language indicators

## Common Tasks

### Adding New Segments
1. Reference official documentation: https://ohmyposh.dev/docs/segments
2. Add segment to appropriate `blocks` array in `oh-my-chill.omp.json`
3. Validate JSON syntax: `python3 -m json.tool oh-my-chill.omp.json > /dev/null`
4. Test rendering: `/tmp/oh-my-posh print primary --config oh-my-chill.omp.json`
5. Run debug mode to verify segment loads: `/tmp/oh-my-posh debug --config oh-my-chill.omp.json`

### Color Customization
1. Colors use hex format (`#ffffff`) or named colors (`red`, `blue`, etc.)
2. Template colors use `<#color>text</>` format
3. Always test color changes visually: `/tmp/oh-my-posh print primary --config oh-my-chill.omp.json`

### Performance Optimization
1. Check segment timing: `/tmp/oh-my-posh debug --config oh-my-chill.omp.json | grep " - .*ms"`
2. Segments should typically take <5ms each
3. Total run duration should be <50ms

## Timing and Expectations

- **JSON validation**: <1 second
- **Theme rendering**: <1 second  
- **Debug mode**: <1 second
- **oh-my-posh download**: ~5 seconds (19MB binary)
- **Theme installation**: Immediate (copy file)

**NEVER CANCEL** these operations - they all complete in seconds, not minutes.

## Dependencies and Installation

### Required Tools
- `python3` - for JSON validation (always available)
- `jq` - alternative JSON validation tool (usually available)
- `curl` - for downloading oh-my-posh binary (always available)
- `git` - for testing git segment functionality (always available)

### oh-my-posh Installation
- Download URL: `https://github.com/JanDeDobbeleer/oh-my-posh/releases/latest/download/posh-linux-amd64`
- Size: ~19MB
- Installation: Download to `/tmp/oh-my-posh` and `chmod +x`
- No system dependencies required

## Error Handling

### Common Issues
1. **JSON syntax errors**: Use `python3 -m json.tool` to identify line numbers and exact error location
2. **Segment not loading**: Check debug output for segment name and timing
3. **Colors not showing**: Verify terminal supports ANSI colors
4. **Git segment empty**: Ensure you're in a git repository with status
5. **Cache errors**: ERROR messages about cache files are normal and can be ignored
6. **wslpath errors**: ERROR about wslpath not found is normal on Linux and can be ignored

### Debugging Steps
1. Always run debug mode first: `/tmp/oh-my-posh debug --config oh-my-chill.omp.json`
2. Check for ERROR/TRACE messages in debug output
3. Verify JSON syntax is valid
4. Test in known working directory (git repo with changes)

## Frequently Used Commands

### Repository Root Structure
```bash
ls -la
# Output:
# drwxr-xr-x 3 runner docker 4096 .
# drwxr-xr-x 3 runner docker 4096 ..
# drwxr-xr-x 7 runner docker 4096 .git
# -rw-r--r-- 1 runner docker   51 README.md
# -rw-r--r-- 1 runner docker 5344 oh-my-chill.omp.json
```

### Theme Configuration Content
The theme includes segments for:
- User session (username@hostname)
- Current path with full directory structure
- Git status with branch and change indicators
- Language environment detection (Node.js, Python, Java, .NET, Go, Rust, etc.)
- Command execution status

All segments use pastel color scheme with Unicode box-drawing characters for visual appeal.