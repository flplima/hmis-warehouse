# Contributing to Open Path HMIS Warehouse

Thank you for your interest in contributing to Open Path! This project helps communities coordinate homeless services and housing resources. Every contribution makes a difference.

## Table of Contents

- [Code of Conduct](#code-of-conduct)
- [How Can I Contribute?](#how-can-i-contribute)
- [Getting Started](#getting-started)
- [Development Workflow](#development-workflow)
- [Pull Request Process](#pull-request-process)
- [Style Guidelines](#style-guidelines)
- [Community](#community)

## Code of Conduct

This project adheres to the [Contributor Covenant Code of Conduct](CODE_OF_CONDUCT.md). By participating, you are expected to uphold this code. Please report unacceptable behavior to opensource@greenriver.com.

## How Can I Contribute?

### Reporting Bugs

Before creating bug reports, please check existing issues to avoid duplicates. When creating a bug report, include:

- **Clear title** describing the issue
- **Steps to reproduce** the behavior
- **Expected behavior** vs. actual behavior
- **Screenshots** if applicable
- **Environment details** (Ruby version, Rails version, browser, OS)

Use the [Bug Report template](.github/ISSUE_TEMPLATE/bug_report.md) when creating issues.

### Suggesting Features

Feature suggestions are welcome! Please use the [Feature Request template](.github/ISSUE_TEMPLATE/feature_request.md) and include:

- **Problem statement** - What problem does this solve?
- **Proposed solution** - How should it work?
- **Alternatives considered** - What other approaches did you consider?
- **Additional context** - Screenshots, mockups, examples

### Your First Contribution

Look for issues labeled:

- [`good first issue`](../../labels/good%20first%20issue) - Simple issues for newcomers
- [`help wanted`](../../labels/help%20wanted) - Issues where we need community help
- [`documentation`](../../labels/documentation) - Documentation improvements
- [`accessibility`](../../labels/accessibility) - Accessibility fixes
- [`testing`](../../labels/testing) - Test coverage improvements

**Not sure where to start?** Here are some beginner-friendly areas:

1. **Documentation** - Improve README, add code comments, fix typos
2. **Accessibility** - Add ARIA labels, improve screen reader support
3. **Test Coverage** - Write specs for untested helper files
4. **Code Cleanup** - Remove TODO comments, fix deprecation warnings

### Code Contributions

We welcome contributions in these areas:

| Area | Examples |
|------|----------|
| **HUD Compliance** | Report updates, data standard changes |
| **Integrations** | New API connections, data imports |
| **Reporting** | New reports, dashboard improvements |
| **Performance** | Query optimization, caching |
| **Security** | Vulnerability fixes, audit improvements |
| **Accessibility** | WCAG compliance, screen reader support |

## Getting Started

### Prerequisites

- Docker and Docker Compose
- Git
- macOS, Linux, or Windows with WSL2

### Quick Setup

```bash
# Clone the repository
git clone https://github.com/greenriver/hmis-warehouse.git
cd hmis-warehouse

# Run automated setup (macOS)
bin/developer/install.sh

# Or manual setup
cp sample.env .env.development.local
docker compose build
docker compose run --rm web bin/setup
```

For detailed setup instructions, see [docs/developer/setup.md](docs/developer/setup.md).

### Running the Application

```bash
# Start all services
docker compose up

# Run in background
docker compose up -d

# View logs
docker compose logs -f web
```

### Running Tests

```bash
# Run full test suite
docker compose run --rm spec

# Run specific test file
docker compose run --rm spec bundle exec rspec spec/models/grda_warehouse/hud/client_spec.rb

# Run tests matching a pattern
docker compose run --rm spec bundle exec rspec -e "deduplication"
```

## Development Workflow

### Branch Naming

```
feature/short-description    # New features
fix/issue-number-description # Bug fixes
docs/what-changed            # Documentation
refactor/what-changed        # Code refactoring
test/what-testing            # Test additions
```

### Making Changes

1. **Fork** the repository
2. **Create a branch** from `production`
3. **Make your changes** with clear, atomic commits
4. **Write/update tests** for your changes
5. **Ensure tests pass** locally
6. **Submit a Pull Request**

### Commit Messages

Write clear, concise commit messages:

```
# Good
Add ARIA labels to admin navigation buttons
Fix N+1 query in client search endpoint
Update LSA report for FY2026 data standards

# Bad
Fixed stuff
WIP
Updates
```

## Pull Request Process

1. **Fill out the PR template** completely
2. **Link related issues** using keywords (Fixes #123, Closes #456)
3. **Ensure CI passes** - All checks must be green
4. **Request review** from maintainers
5. **Address feedback** promptly
6. **Squash commits** if requested

### PR Checklist

Before submitting:

- [ ] Tests pass locally (`docker compose run --rm spec`)
- [ ] RuboCop passes (`bundle exec rubocop`)
- [ ] No new security warnings (`bundle exec brakeman`)
- [ ] Documentation updated (if applicable)
- [ ] Changelog updated (for significant changes)

### Review Timeline

- **Initial response**: Within 3-5 business days
- **Review cycle**: Depends on complexity
- **Merge**: After approval and CI passes

## Style Guidelines

### Ruby Style

We use RuboCop for Ruby style enforcement. Key conventions:

```ruby
# Use trailing commas in multi-line collections
users = [
  'Alice',
  'Bob',
  'Charlie',  # <- trailing comma
]

# Prefer postfix conditionals for single-line statements
return if user.nil?

# Use Arel over raw SQL
Client.where(arel_table[:created_at].gt(1.week.ago))
```

See [docs/code_patterns_and_conventions.md](docs/code_patterns_and_conventions.md) for detailed guidelines.

### JavaScript Style

- Use Stimulus controllers for interactivity
- Prefer Turbo over custom AJAX
- ESLint configuration in `package.json`

### Testing Style

```ruby
# Use descriptive context blocks
RSpec.describe Client do
  describe '#full_name' do
    context 'when first and last name are present' do
      it 'returns combined name' do
        # ...
      end
    end
  end
end
```

## Architecture Overview

Understanding the codebase structure:

```
app/
├── models/grda_warehouse/    # Core warehouse models
│   └── hud/                  # HUD data standard models
├── controllers/              # Request handlers
├── views/                    # HAML templates
└── javascript/               # Stimulus controllers

drivers/                      # Modular feature plugins (88 total)
├── hud_apr/                  # HUD APR report
├── hud_lsa/                  # LSA report
├── hmis_csv_importer/        # CSV import
└── ...

docs/
├── developer/                # Setup guides
├── adr/                      # Architecture decisions
└── features/                 # Feature documentation
```

### Key Concepts

- **Data Sources**: External HMIS systems that provide data
- **Warehouse Clients**: Deduplicated "golden records"
- **Drivers**: Self-contained feature modules
- **Cohorts**: Groups of clients for tracking

## Community

### Getting Help

- **GitHub Discussions**: Ask questions, share ideas
- **Issues**: Report bugs, request features
- **Documentation**: [docs/](docs/) directory

### Communication Guidelines

- Be respectful and inclusive
- Assume good intentions
- Focus on the problem, not the person
- Help others learn

## Recognition

Contributors are recognized in:

- GitHub contributor graph
- Release notes for significant contributions
- Annual contributor acknowledgments

## License

By contributing, you agree that your contributions will be licensed under the [GNU General Public License v3.0](LICENSE.md).

---

Thank you for contributing to Open Path! Your work helps communities end homelessness.
