👥 Member 4: The "Guardian" (CI/CD & Reporting)
Role: Showing how we automate everything so humans don't make mistakes.

1. Setup
npm install mochawesome

2. The Code (.github/workflows/tests.yml)
   name: Wildlife System CI-CD

# This tells the robot when to wake up
on: 
  push:
    branches: [ main, develop ] # It will run on both branches
  pull_request:
    branches: [ main, develop ]

jobs:
  test-and-report:
    runs-on: ubuntu-latest # The robot's computer (Linux)
    
    steps:
      # Step 1: Download your code from GitHub to the robot's cloud computer
      - name: 📥 Checkout Code
        uses: actions/checkout@v4

      # Step 2: Install Node.js
      - name: 🟢 Setup Node.js
        uses: actions/setup-node@v4
        with:
          node-version: '20'

      # Step 3: Install all your project libraries (Mocha, Chai, etc.)
      - name: 📦 Install Dependencies
        run: |
          cd backend
          npm install

      # Step 4: Run the actual tests and create the visual report
      - name: 🚀 Run Mocha Tests
        run: |
          cd backend
          npm test

      # Step 5: Save the beautiful HTML report so you can download it later
      - name: 📊 Upload Test Report
        if: always() # This ensures the report is saved even if tests fail
        uses: actions/upload-artifact@v4
        with:
          name: mocha-html-report
          path: backend/mochawesome-report/

3. How it works (Simple English)
CI/CD: This "YAML" file tells GitHub to hire a robot. Every time we "push" code to GitHub, the robot automatically runs all our tests.
Reporting: Using mochawesome, the robot creates a beautiful HTML report with green and red charts.
4. Why it's important
Consistency: Humans forget to run tests; robots never forget.
Reporting: The visual report makes it easy for the whole team to see exactly what is broken without reading thousands of lines of code.
