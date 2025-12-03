# CI-CD-PIPELINE-SETUP



# 🚀 CI/CD Pipeline Execution Using GitHub Actions (Complete Steps)

## 🔹  1  Create Project Repository & Add Web Page

1. Go to **GitHub → New Repository**
2. Fill details:

   * Repository Name: `ci-cd-demo` (or any name)
   * Visibility: **Public**
   * Check **“Add a README”**
3. Click **Create Repository**

### ➤ Add `index.html` file

1. Inside the repository → click **Add file → Create new file**
2. File name: `index.html`
3. Paste the content:

```html
<!DOCTYPE html>
<html>
<head>
  <title>CI/CD Demo</title>
</head>
<body>
  <h1>Hello from CI/CD Pipeline!</h1>
  <p>Deployment executed successfully 🎉</p>
</body>
</html>
```

4. Scroll down → click **Commit changes**

---

## 🔹  2  Configure Deployment Target (GitHub Pages)

1. Open the repo → **Settings**
2. In left sidebar → select **Pages**
3. Under **Build and deployment → Source** select **GitHub Actions**
4. Save (if needed)

---

## 🔹  3  Create the CI/CD Pipeline Workflow

1. Go to **Actions** tab

2. Click **“New workflow”**

3. Scroll down → click **“set up a workflow yourself”**

4. It will open a file editor:
   `.github/workflows/pages.yml`

5. Delete all existing text and paste this:

```yaml
name: CI/CD for Demo Site

on:
  push:
    branches: [ "main" ]

permissions:
  contents: read
  pages: write
  id-token: write

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repository
        uses: actions/checkout@v4

      - name: Simulate Build
        run: echo "Build process for static site completed."

      - name: Upload artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: .

  deploy:
    runs-on: ubuntu-latest
    needs: build
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}

    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4
```

6. Click **Commit changes**

---

## 🔹  4  Verify First Automatic Deployment

1. Go to **Actions** tab

2. The workflow **starts automatically** because you just committed a file

3. Verify both jobs:

   * `build` → ✔
   * `deploy` → ✔

4. After success:

   * Go to: **Settings → Pages**
   * Copy the website URL (example):
     `https://<username>.github.io/ci-cd-demo/`

5. Open the URL → Page should display:

> Hello from CI/CD Pipeline!
> Deployment executed successfully 🎉

---

## 🔹  5  Modify Project to Test CI/CD Again

### ➤ Update the `index.html` file

1. Go to `index.html` in the repo
2. Click **Edit**
3. Replace the `<h1>` line with:

```html
<h1>CI/CD Pipeline Working After Update ✔</h1>
```

4. Scroll down → **Commit changes**

---

## 🔹  6  Confirm Automated Pipeline Triggered Again

1. Go to **Actions**
2. You will see the pipeline running again **automatically** (triggered by commit)
3. Wait until both jobs turn **green (✔)**

---

## 🔹  7  Validate Second Deployment

1. Open the GitHub Pages URL again
2. **Refresh the page**
3. New updated content should appear:

> CI/CD Pipeline Working After Update ✔


# 🎉 Final Expected Outcome

You have **successfully executed a complete CI/CD pipeline** using GitHub Actions with:

✔ Repository created
✔ Web application added
✔ GitHub Pages selected as deployment target
✔ CI/CD workflow built & committed
✔ First automatic deployment tested
✔ Code updated & pipeline triggered again
✔ Second deployment verified live
