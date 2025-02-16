---

# React Native E2E Testing & EAS Build  

This repository contains a **React Native** application configured to run **end-to-end (E2E) tests** using **Maestro** in a **CI/CD pipeline** via GitHub Actions. Additionally, it utilizes **Expo EAS (Expo Application Services)** to manage the build process.

## 🚀 Features  

- End-to-end testing with **Maestro**  
- CI/CD automation using **GitHub Actions**  
- Build and distribute app using **Expo EAS**  

---

## 📌 Prerequisites

Ensure you have the following installed before proceeding:

- **Node.js** (Recommended: latest LTS)
- **npm** or **yarn**
- **Expo CLI** (`npm install -g expo-cli`)
- **Maestro CLI** (`curl -Ls https://get.maestro.mobile.dev | bash`)
- **EAS CLI** (`npm install -g eas-cli`)
- **GitHub Actions** enabled for CI/CD

---

## 📦 Installation

Clone the repository and install dependencies:

```bash
git clone https://github.com/your-repo-name.git
cd your-repo-name
npm install  # or yarn install
```

---

## 🎭 Setting Up Maestro

Install Maestro CLI if not already installed:

```bash
curl -Ls https://get.maestro.mobile.dev | bash
```

Verify installation:

```bash
maestro -v
```

To run tests locally:

```bash
maestro test e2e/tests.yaml
```

---

## 🏗️ Setting Up EAS

Login to Expo (if not already logged in):

```bash
eas login
```

Configure EAS for the project:

```bash
eas init
```

To build the app:

```bash
eas build --platform android  # or ios
```

To submit the build:

```bash
eas submit --platform android  # or ios
```

---

## 🔄 Running E2E Tests in GitHub Actions

The repository includes a **GitHub Actions workflow** to run Maestro tests in CI/CD.

### Example Workflow (`.github/workflows/ci.yml`)

```yaml
name: E2E Tests & Expo Build

on: [push, pull_request]

jobs:
  e2e-tests:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Setup Node.js
        uses: actions/setup-node@v3
        with:
          node-version: 18

      - name: Install dependencies
        run: npm install

      - name: Install Maestro
        run: curl -Ls https://get.maestro.mobile.dev | bash

      - name: Run E2E Tests
        run: maestro test e2e/tests.yaml

  build:
    needs: e2e-tests
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Setup Node.js
        uses: actions/setup-node@v3
        with:
          node-version: 18

      - name: Install dependencies
        run: npm install

      - name: Install EAS CLI
        run: npm install -g eas-cli

      - name: Login to Expo
        run: eas login --token ${{ secrets.EXPO_TOKEN }}

      - name: Build App
        run: eas build --platform android --non-interactive
```

---

## 🔑 Environment Variables

To enable **Expo EAS** authentication in CI/CD, add the following environment variable in **GitHub Secrets**:

- `EXPO_TOKEN`: Your Expo authentication token (Generate using `expo login` → `expo token:create`)

---

## 📖 Additional Documentation

- [Maestro Documentation](https://maestro.mobile.dev)
- [Expo EAS Documentation](https://docs.expo.dev/eas/)
- [GitHub Actions Documentation](https://docs.github.com/en/actions)

---

## 🛠️ Troubleshooting

- If Maestro fails to run tests, ensure `adb` (Android Debug Bridge) is installed.
- If EAS builds fail, check your Expo account credentials.

---

## 🏁 Conclusion

This repository enables streamlined **E2E testing** and **CI/CD automation** for a React Native application using **Maestro** and **Expo EAS**. 🚀

---

Would you like me to add anything specific, such as instructions for running tests on iOS or troubleshooting Expo builds? 😊
