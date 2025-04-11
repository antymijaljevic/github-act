# Local GitHub Actions Environment

This project demonstrates how to set up and run GitHub Actions workflows locally using `act`. This allows you to test your CI/CD pipelines before pushing them to GitHub.

## Prerequisites

- macOS (tested on Apple Silicon)
- [Homebrew](https://brew.sh/) (for package management)
- [Docker](https://www.docker.com/) (for running the GitHub Actions runners)

## Installation

1. Install `act` using Homebrew:
   ```bash
   brew install act
   ```

2. Make sure Docker is installed and running on your system.

## Project Structure

```
.
├── .github/
│   └── workflows/
│       └── test.yml      # GitHub Actions workflow file
└── README.md             # This file
```

## Workflow Configuration

The project includes a basic workflow file (`.github/workflows/test.yml`) that:
- Triggers on push and pull request events to the main branch
- Runs on Ubuntu latest
- Performs a simple "Hello, world!" test

## Running Workflows Locally

1. Initialize Git repository (if not already done):
   ```bash
   git init
   git add .
   git commit -m "Initial commit"
   ```

2. Run the workflow:
   ```bash
   act --container-architecture linux/amd64
   ```

### Common Commands

- List available workflows:
  ```bash
  act -l
  ```

- Run specific events:
  ```bash
  act push              # Simulate push event
  act pull_request      # Simulate pull request event
  ```

- Run on specific branch:
  ```bash
  act -b <branch-name>
  ```

## Troubleshooting

1. **Docker Issues**
   - Make sure Docker is running
   - Check Docker daemon status: `docker info`

2. **M1/M2 Mac Specific**
   - Always use `--container-architecture linux/amd64` flag
   - If you encounter issues, try:
     ```bash
     docker system prune -a
     act --container-architecture linux/amd64 --pull
     ```

3. **Git Issues**
   - Ensure you're in a Git repository
   - Make sure you have at least one commit

## Best Practices

1. **Image Selection**
   - First run will prompt you to choose an image size
   - Recommended: Medium size (~500MB)
   - Large size (17GB) if you need full GitHub runner compatibility

2. **Workflow Development**
   - Test locally before pushing to GitHub
   - Use environment variables for sensitive data
   - Keep workflows modular and reusable

3. **Performance**
   - Use Docker cache effectively
   - Clean up unused images periodically:
     ```bash
     docker system prune
     ```

## Limitations

- Some GitHub Actions features might not work exactly the same locally
- Secrets and environment variables need to be configured separately
- Some third-party actions might not be fully compatible

## Resources

- [act Documentation](https://github.com/nektos/act)
- [GitHub Actions Documentation](https://docs.github.com/en/actions)
- [Docker Documentation](https://docs.docker.com/)

## License

This project is open source and available under the [MIT License](LICENSE). 