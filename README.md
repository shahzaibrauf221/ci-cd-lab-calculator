# CI/CD Lab: Bulletproof Calculator

[![Python CI Pipeline](https://github.com/YOUR_USERNAME/YOUR_REPO_NAME/actions/workflows/ci.yml/badge.svg)](https://github.com/YOUR_USERNAME/YOUR_REPO_NAME/actions/workflows/ci.yml)

> **Note:** Replace `YOUR_USERNAME` and `YOUR_REPO_NAME` in the badge URL above with your actual GitHub username and repository name.

---

## 📁 Project Structure

```
ci-cd-lab-calculator/
├── .github/
│   └── workflows/
│       ├── ci.yml      # Continuous Integration pipeline
│       └── cd.yml      # Continuous Delivery pipeline
├── src/
│   └── calculator.py   # Main application code
├── tests/
│   └── test_calculator.py  # Unit tests
├── requirements.txt
└── README.md
```

---

# Part 1: Continuous Integration (CI)

## 🔧 Step 1: Setup

1. Click the **Actions** tab in your GitHub repository.
2. You should see a workflow run listed (triggered by your initial push).
3. Click on the workflow run to see the steps. Ensure all steps have a green checkmark ✅.

## 🧪 Step 2: The "Happy Path"

1. Open `src/calculator.py`.
2. Add a small comment to the file (e.g., `# This is a change`).
3. Commit and push the change to GitHub.
4. Go to the **Actions** tab immediately. Watch the pipeline start automatically.
5. Observe how it sets up Python, installs dependencies, runs linter, and runs the tests. It should pass.

## 💥 Step 3: Break the Build!

Now, let's see what happens when we make a mistake.

1. Open `src/calculator.py`.
2. Change the `add` function so it is **incorrect**:

```python
def add(x, y):
    return x - y  # This is a bug!
```

3. Commit and push this change.
4. Go to the **Actions** tab.
5. **Observe:** The pipeline will fail (Red X ❌).
6. Click into the failure details and find the specific test that failed (`test_add`).

## 🚑 Step 4: Fix the Build

1. Revert the change in `src/calculator.py` to fix the bug:

```python
def add(x, y):
    return x + y
```

2. Commit and push.
3. Verify in the **Actions** tab that the build is Green ✅ again.

---

# Part 2: Continuous Delivery (CD)

## 📦 Step 1: Understanding the Trigger

Look at `cd.yml`. Notice it doesn't run on every push. It waits for a **Tag**. In the professional world, tags represent specific versions (like v1.0 or v2.4).

## 🚀 Step 2: Creating your first Release

1. Ensure your code is working and all tests pass.
2. Open your terminal and run these commands to "tag" your code:

```bash
git tag v1.0
git push origin v1.0
```

3. Go to the **Actions** tab. You will see a new workflow named "Continuous Delivery" starting!
4. Once it finishes, go to the **main page** of your GitHub repository.
5. Look at the right-hand sidebar under **"Releases."** You should see `v1.0`.
6. Click it. You will find a `.tar.gz` file—this is your "shipped" software!

## 🧪 Step 3: The "Safety Net"

1. Break your code again in `src/calculator.py` (e.g., change `return x + y` to `return x * 99`).
2. Try to ship this broken version:

```bash
git add .
git commit -m "Attempting to ship broken code"
git tag v1.1
git push origin v1.1
```

3. **Observe:** The CD pipeline will fail at the "Sanity Check" step.

---

## 📝 Available Functions

| Function | Description |
|----------|-------------|
| `add(x, y)` | Returns sum of x and y |
| `subtract(x, y)` | Returns difference of x and y |
| `multiply(x, y)` | Returns product of x and y |
| `divide(x, y)` | Returns division of x by y (raises error if y=0) |
| `power(x, y)` | Returns x raised to power y |

---

## 🎯 Exercises Completed

- [x] Exercise 1: Feature Expansion (power function added)
- [x] Exercise 2: Strict Gatekeeper (float return enforced)
- [x] Exercise 3: Linting (flake8 added to CI)
- [x] Exercise 5: Artifact includes requirements.txt
- [x] Exercise 1 (CD): Release notes include actor name

---

## 📚 Learning Outcomes

- Understanding CI/CD pipelines
- Automated testing with GitHub Actions
- Code quality with linting
- Version tagging and releases
- Protecting codebase from breaking changes
