# React Investment Calculator

A **React + Vite** web application that calculates and visualises the year-by-year growth of an investment based on user-defined parameters. Enter your initial investment amount, annual contribution, expected rate of return, and investment duration to instantly see a detailed breakdown of how your money grows over time.

## Features

- **Real-time calculation** — results update instantly as you change any input field
- **Year-by-year breakdown** — a results table showing for each year:
  - Total investment value at end of year
  - Interest earned in that year
  - Cumulative total interest earned
  - Total capital invested (principal + contributions)
- **Input validation** — displays an error message when the duration is less than 1 and hides the results table until the input is valid
- **USD currency formatting** — all monetary values are formatted using the browser's built-in `Intl.NumberFormat` API

## Tech Stack

| Technology | Version | Purpose |
|---|---|---|
| [React](https://react.dev/) | ^19 | UI component library |
| [Vite](https://vitejs.dev/) | ^8 | Build tool and dev server |
| [ESLint](https://eslint.org/) | ^10 | Code linting |
| eslint-plugin-react | ^7 | React-specific lint rules |
| eslint-plugin-react-hooks | ^7 | Hooks lint rules |
| eslint-plugin-react-refresh | ^0.5 | Fast Refresh lint rules |

## Project Structure

```
src/
├── components/
│   ├── Header.jsx       # App title / logo header
│   ├── UserInput.jsx    # Four numeric input fields
│   └── Results.jsx      # Year-by-year results table
├── util/
│   └── investment.js    # calculateInvestmentResults() helper + currency formatter
├── App.jsx              # Root component — state management and layout
├── index.jsx            # React DOM entry point
└── index.css            # Global styles
```

## Getting Started

### Prerequisites

- [Node.js](https://nodejs.org/) (LTS recommended)
- npm (bundled with Node.js)

### Installation & Development

```bash
# Install dependencies
npm install

# Start the development server (http://localhost:5173 by default)
npm run dev
```

### Other Available Scripts

```bash
# Lint the codebase
npm run lint

# Build for production
npm run build

# Preview the production build locally
npm run preview
```

## How It Works

The core calculation logic lives in `src/util/investment.js`. For each year of the investment duration it:

1. Computes the interest earned as `investmentValue × (expectedReturn / 100)`
2. Adds that interest plus the annual contribution to the running investment value
3. Pushes an entry `{ year, interest, valueEndOfYear, annualInvestment }` to an array

The `Results` component derives **Total Interest** and **Invested Capital** from this array and renders them in a formatted table using the `Intl.NumberFormat` USD currency formatter.
