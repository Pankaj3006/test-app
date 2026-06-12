# quiz-cli

## Overview

`quiz-cli` is an interactive command-line quiz game built with Node.js. It loads quiz questions from a local JSON file, lets the user choose a category and question count, and then walks through the quiz with scoring, explanations, and a final results summary.

The repository is implemented as a small ES Modules-based CLI application with no third-party runtime dependencies.

## Business Problem

This project provides a lightweight, terminal-based learning tool for practicing programming fundamentals. It is useful for:

- self-study and revision
- quick knowledge checks in the terminal
- demonstrating Node.js CLI patterns
- learning how to structure a small ES module application

## Solution Overview

The application:

1. Loads question data from `data/questions.json`
2. Prompts the user to select a category
3. Lets the user choose how many questions to answer
4. Displays each question as a multiple-choice prompt
5. Scores the quiz and shows explanations for incorrect answers
6. Offers the option to replay the game

## Key Features

### Core Features

- Interactive terminal quiz experience
- Category-based question selection
- Configurable number of questions per run
- Randomized question order
- Immediate feedback after each answer
- Final score summary and review of incorrect answers

### Administrative / Support Features

- Colorized terminal output using ANSI escape codes
- Clear progress indicator during the quiz
- Reusable input-handling helpers
- Modular quiz logic separated from entrypoint code

### Integration Features

- Loads quiz content from a local JSON data file
- Uses Node.js built-in `readline`, `fs/promises`, `path`, and `url` modules

### Security Features

- No network access or external service dependencies are required
- No user accounts, secrets, or credentials are involved

## Technology Stack

- **Language:** JavaScript (ES Modules)
- **Runtime:** Node.js >= 18.0.0
- **CLI/Input:** Node.js `readline`
- **File I/O:** Node.js `fs/promises`
- **Data Format:** JSON
- **Package Manager:** npm
- **License:** MIT

## Architecture Overview

The application uses a simple layered CLI architecture:

- **Entry point (`index.js`)** orchestrates startup, question loading, user flow, and replay logic.
- **Input layer (`src/input.js`)** wraps `readline` interactions behind reusable helpers.
- **Domain/game logic (`src/quiz.js`)** contains the quiz class, scoring, answer tracking, and results rendering.
- **Presentation helpers (`src/colors.js`)** format terminal output with ANSI colors.
- **Data layer (`data/questions.json`)** stores quiz categories and questions.

### Data Flow

1. `index.js` reads `data/questions.json`
2. The user selects a category and question count
3. `Quiz` shuffles questions and asks them one by one
4. Results are calculated and printed to the terminal
5. The user may replay the quiz

### Deployment Model

- Local CLI application
- No server, container, or cloud deployment configuration is present in this repository

## File Structure

```text
.
├── index.js
├── package.json
├── data/
│   └── questions.json
└── src/
    ├── colors.js
    ├── input.js
    └── quiz.js
```

### Major Folders and Files

#### `data/`
- **Purpose:** Holds quiz content
- **Responsibilities:** Stores categories, questions, answer keys, and explanations
- **Key Files:** `questions.json`
- **Dependencies:** Read by `index.js` at runtime
- **Setup Rules:** Keep JSON valid and preserve the expected structure (`categories -> questions`)

#### `src/`
- **Purpose:** Contains application modules
- **Responsibilities:** Input handling, quiz logic, and terminal formatting
- **Key Files:** `colors.js`, `input.js`, `quiz.js`
- **Dependencies:** Used by `index.js`
- **Setup Rules:** Maintain ES module syntax (`import` / `export`)

#### Root files
- **Purpose:** Application entry and package metadata
- **Responsibilities:** Start the CLI and define npm scripts
- **Key Files:** `index.js`, `package.json`
- **Dependencies:** Node.js runtime
- **Setup Rules:** Run from the repository root

## Prerequisites

- Node.js **18.0.0 or later**
- npm (bundled with Node.js)
- A terminal that supports ANSI colors is recommended

## Installation

```bash
git clone <repository-url>
cd test-app
npm install
```

### Build Commands

There is no build step defined in this repository.

## Configuration

No environment variables or external configuration files are required.

### Environment Variables

None documented or required.

## Getting Started

1. Install prerequisites
2. Clone the repository
3. Install dependencies with `npm install`
4. Start the quiz with `npm start`

## Running the Application

```bash
npm start
```

This runs:

```bash
node index.js
```

### Startup Flow

- The app clears the terminal and shows a banner
- You choose a quiz category
- You choose how many questions to answer
- You answer each multiple-choice question
- The app shows your score and review notes
- You can choose to play again

## Usage Examples

### Example workflow

```bash
npm start
```

Then follow the prompts in the terminal:

- select a category
- select the question count
- enter the number for your answer
- press Enter to continue between questions
- choose whether to play again

### Common Commands

```bash
npm start   # Run the quiz
npm test    # Run Node.js test runner
```

## API Documentation

This project does not expose an HTTP API, REST API, or GraphQL API.

Instead, it provides internal module APIs:

- `createInterface()`, `prompt()`, `select()`, `confirm()`, `pressEnter()` in `src/input.js`
- `Quiz` class in `src/quiz.js`
- color helper functions in `src/colors.js`

## Testing

The repository defines the following test script:

```bash
npm test
```

This executes:

```bash
node --test
```

### Verification Steps

After running the application, verify that:

- the banner is displayed
- categories are listed correctly
- answer selection works with numeric input
- correct/incorrect feedback is shown
- results summary appears at the end
- replay prompt works as expected

## Development Guide

### Local Development

- Edit quiz content in `data/questions.json`
- Update terminal formatting in `src/colors.js`
- Adjust prompt behavior in `src/input.js`
- Update scoring or result logic in `src/quiz.js`
- Modify startup flow in `index.js`

### Code Style

- Uses ES module syntax
- Uses async/await for user interaction and file loading
- Keeps CLI logic separated into focused modules

### Debugging

If the app exits unexpectedly:

- verify Node.js version is 18 or newer
- confirm `data/questions.json` is valid JSON
- ensure `index.js` is run from the repository root
- inspect the error stack trace printed in the terminal

## Deployment

### Docker Deployment

No Dockerfile or container configuration is present.

### Kubernetes Deployment

No Kubernetes manifests are present.

### Cloud Deployment

No cloud infrastructure files are present.

## CI/CD

No CI/CD configuration is present in this repository.

## Monitoring and Logging

- The application logs directly to the terminal
- Errors are printed with stack traces in the catch block of `index.js`
- No external logging or monitoring system is configured

## Security Considerations

- The project does not handle credentials, tokens, or sensitive user data
- All quiz data is local and bundled with the repository
- There is no network connectivity or remote dependency at runtime

## Troubleshooting

### `node: bad option: --test`

Use Node.js 18 or newer.

### JSON parsing errors on startup

Check `data/questions.json` for invalid JSON syntax.

### Colors do not display correctly

Some terminals do not fully support ANSI escape codes. Try a different terminal emulator.

### Quiz exits immediately

Ensure you are running from the repository root so `data/questions.json` can be found.

## Known Limitations

- Question content is static and stored locally in `data/questions.json`
- No persistence of scores or user history
- No authentication or multi-user support
- No automated test files are present in the repository at the time of review
- No linting or formatting configuration is provided

## Contributing

Contributions should follow the existing module structure and keep the CLI experience simple and dependency-free.

Suggested contribution areas:

- add more quiz categories
- add more questions and explanations
- improve test coverage
- add linting/formatting tooling
- add persistence for scores or progress

## Roadmap

Not defined in the repository.

Potential next steps:

- add automated tests
- add more question categories
- add score history or persistence
- introduce linting and formatting scripts
- package the CLI for distribution

## License

MIT

## Support

This repository does not include formal support channels.

If you are maintaining the project, consider adding one or more of the following:

- issue templates
- contributor guidelines
- troubleshooting notes
- release notes

## Assumptions

- The repository is intended to be a Node.js CLI quiz application based on `package.json` and `index.js`.
- The `npm test` script is available, but no test files are currently included in the repository snapshot.
- No deployment targets, CI systems, or external services are configured in the repository.

## Missing Documentation

The following items are not documented in the repository and should be added if available:

- detailed question authoring rules for `data/questions.json`
- contribution workflow
- test coverage expectations
- release/versioning strategy
- issue/PR templates
- support contact or maintainer information
- deployment or packaging instructions
