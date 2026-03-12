# UtilityCalc — Simple Everyday Calculators

![SvelteKit](https://img.shields.io/badge/Framework-SvelteKit-FF3E00?logo=svelte&logoColor=white)
![TailwindCSS](https://img.shields.io/badge/Styled_with-TailwindCSS-38BDF8?logo=tailwindcss&logoColor=white)
![Bun](https://img.shields.io/badge/Runtime-Bun-000000?logo=bun&logoColor=white)
![GitHub Pages](https://img.shields.io/badge/Hosting-GitHub_Pages-181717?logo=github&logoColor=white)
![Build Status](https://img.shields.io/github/actions/workflow/status/iNoles/utilitycalc/main.yml?label=Build)
![License](https://img.shields.io/github/license/iNoles/utilitycalc)

UtilityCalc is a collection of clean, fast, and mobile‑friendly calculators built with SvelteKit 2, Tailwind CSS v4, and Bun. The suite includes tools for gas mileage, fuel savings comparison, amortization, and BAC estimation, all deployed as a fully static site on GitHub Pages.

## Features

- Responsive layout with a unified header and mobile navigation
- Fully static prerendering using @sveltejs/adapter-static
- Correct base‑path routing for GitHub Pages
- Bun‑powered development and build workflow
- Clean, accessible UI with consistent component styling

## Tech Stacks

- SvelteKit 2 for routing and application structure
- Tailwind CSS v4 for styling
- Bun for fast installs and builds
- GitHub Actions for CI and deployment
- GitHub Pages for hosting

### Installation

1. Clone the repository:

   ```bash
   git clone https://github.com/iNoles/utilitycalc.git
   cd utilitycalc
   ```

2. Install dependencies using bun:

   ```bash
   bun install
   ```

### Available Scripts

- `bun dev`: Start the development server.
- `bun build`: Create a production build.
- `bun preview`: Preview the production build.

### Contributing

Contributions are welcome! Here's how you can help:

1. Fork the repository.
2. Create your feature branch (`git checkout -b feature/YourFeature`).
3. Commit your changes (`git commit -m 'Add YourFeature'`).
4. Push to the branch (`git push origin feature/YourFeature`).
5. Open a pull request.
