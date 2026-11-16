# Contributing to opensam

Thank you for helping. Bug reports, fixes, documentation and new ideas are all welcome.

## Before you start

- **Found a bug?** Open an issue with the bug report template. Say which project
  (`full-mesh`, `mediasoup` or `v2ai`), what you ran, what you expected and what happened.
- **Want to change something bigger?** Open an issue first and describe the change,
  so we can agree on the approach before you spend time on it.
- **Small fixes** (typos, docs, an obvious bug) can go straight to a pull request.

## Working on a change

1. Fork the repository and create a branch from `main`.
2. Make your change inside the project folder it belongs to. Each project is
   self-contained, with its own `docker-compose.yml` and README.
3. Run the project with `docker compose up --build` and check your change works.
4. For the Node.js parts, run the linter in that project folder (`npx eslint .`).
5. Update the project's README if you changed how it is set up or run.

## Pull requests

- Keep each pull request to one change, and explain what it does and why.
- Link the issue it fixes, if there is one.
- Never commit secrets: API keys belong in `.env` files, which are git-ignored.
- Every pull request is reviewed before it is merged.

## Licence

By contributing, you agree that your contribution is licensed under the
[MIT licence](LICENSE) that covers this repository.
