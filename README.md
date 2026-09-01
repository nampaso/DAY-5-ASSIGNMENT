# Technical Writing Lab

This repository contains the technical documentation submission for the **Technical Writing Lab**, structured into three core modules: an end-user manual procedure, a REST API endpoint specification, and a peer technical critique framework.

---

## 📋 Table of Contents
- [Module 1: User Manual Procedure](#module-1-user-manual-procedure)
- [Module 2: REST API Reference Documentation](#module-2-rest-api-reference-documentation)
- [Module 3: Peer Critique & Evaluation Framework](#module-3-peer-critique--evaluation-framework)

---

## Module 1: User Manual Procedure

### Selected Task
**Setting Up a GitHub Repository from Scratch and Making Your First Commit**

### Audience Profile
First-semester computer science student with general computer literacy (keyboard navigation, file opening), but no prior CLI or version control experience.

---

### Prerequisites
Before starting this guide, ensure you have the following:
* A web browser with an active account created on [GitHub.com](https://github.com).
* Git installed on your computer (verify by opening Terminal or Command Prompt and entering `git --version`).
* Visual Studio Code (VS Code) or a similar text editor installed.
* A local folder containing at least one project file (such as `index.html` or `script.py`).

---

### Step-by-Step Procedure

1. **Log in to GitHub and navigate to the creation page.**
   * Open your web browser, navigate to [github.com](https://github.com), log in to your account, click the **`+`** icon in the upper-right corner of the top navigation bar, and select **New repository**.
   * *Expected Result:* You are redirected to the **"Create a new repository"** setup page.

2. **Name your repository.**
   * In the **Repository name** input field, type `my-first-repo` (use lowercase letters and hyphens instead of spaces).
   * *Expected Result:* A green checkmark icon appears next to the field, confirming the repository name is available under your account.

3. **Configure repository visibility and initialize settings.**
   * Scroll down to the **Public/Private** options, select **Public**, leave all initialization options unchecked (**Add a README file**, **Add .gitignore**, and **Choose a license** must remain unchecked), and click the green **Create repository** button.
   * *Expected Result:* GitHub creates the empty repository and displays a page titled **"Quick setup"** containing your repository's unique HTTPS URL.

4. **Copy your remote repository URL.**
   * On the **"Quick setup"** page, verify that the **HTTPS** tab is selected, then click the **Copy to clipboard** button (the icon depicting two overlapping squares) next to the URL field.
   * *Expected Result:* The URL string (e.g., `https://github.com/your-username/my-first-repo.git`) is copied to your clipboard.

5. **Open your local project directory in the Terminal.**
   * Open Terminal (macOS/Linux) or Command Prompt (Windows), type `cd` followed by a space, drag your local project folder into the terminal window, and press **Enter**.
   * *Expected Result:* The terminal prompt updates its path indicator to match your local project folder directory.

6. **Initialize Git inside your local directory.**
   * Type `git init` into the terminal prompt and press **Enter**.
   * *Expected Result:* The terminal outputs the text: `Initialized empty Git repository in /path/to/your/folder/.git/`.

7. **Stage all files for tracking.**
   * Type `git add .` into the terminal prompt and press **Enter**.
   * *Expected Result:* Git stages all files in your current directory without error messages. You can verify this by typing `git status` to see your files listed in green under "Changes to be committed".

8. **Create your first commit.**
   * Type `git commit -m "Initial commit"` into the terminal prompt and press **Enter**.
   * *Expected Result:* The terminal outputs a commit confirmation message showing the root commit hash, the number of files changed, and insertions made.

9. **Rename your default local branch to main.**
   * Type `git branch -M main` into the terminal prompt and press **Enter**.
   * *Expected Result:* Git updates your default local branch name to `main` with no output errors returned.

10. **Link your local repository to GitHub.**
    * Type `git remote add origin ` into the terminal prompt, paste the URL copied in Step 4, and press **Enter**.
    * *Expected Result:* The remote pointer named `origin` is attached silently to your local repository configuration.

11. **Push your local commit to GitHub.**
    * Type `git push -u origin main` into the terminal prompt and press **Enter**. (If prompted, authenticate via your browser or GitHub Personal Access Token).
    * *Expected Result:* The terminal displays progress percentages, followed by `Branch 'main' set up to track remote branch 'main' from 'origin'`. Refreshing your repository page on GitHub now displays your uploaded project files.

---

### Visual Screenshot Description

> **Figure 1: GitHub Quick Setup Page for Empty Repositories**
> 
> * **Location in Flow:** Insert immediately after **Step 3** and prior to **Step 4**.
> * **Visual Elements to Display:** A full-width browser capture showing the top section of the newly created GitHub repository page.
> * **Specific Annotations:**
>   1. A red callout box highlighting the **HTTPS** toggle tab.
>   2. A blue callout arrow pointing directly to the **Copy to clipboard** button next to the repository URL string `https://github.com/username/my-first-repo.git`.
>   3. A highlighted banner over the section titled **"…or push an existing repository from the command line"** to guide students connecting a local folder.

---

### Troubleshooting Note

> ⚠️ **Troubleshooting: `error: src refspec main does not match any`**
> 
> **Why this happens:** This error occurs when you run `git branch -M main` or `git push -u origin main` before making an initial commit. Git cannot rename or push a branch that contains no commits.
> 
> **How to fix it:**
> 1. Verify if you have staged files by running `git status`.
> 2. Stage your files by entering `git add .` and pressing **Enter**.
> 3. Create your initial commit by entering `git commit -m "Initial commit"` and pressing **Enter**.
> 4. Retry the push command: `git push -u origin main`.

---

## Module 2: REST API Reference Documentation

### Endpoint Specification

`POST /api/v1/projects/{project_id}/tasks`

Creates a new task record within a specified project resource.

---

### Overview & Authentication

This endpoint provisions a new task entity attached to a parent project identified by `project_id`. The client must provide a valid JSON object containing task parameters in the request body.

* **Authentication Required:** Yes (Bearer Token)
* **Access Level:** Project Contributor, Project Admin, or System Administrator
* **Rate Limit:** 60 requests per minute per authenticated user

---

### HTTP Request Headers

| Header Name | Type | Required? | Description | Example |
| :--- | :--- | :--- | :--- | :--- |
| `Authorization` | String | **Required** | OAuth 2.0 Bearer token for identity verification. | `Bearer eyJhbGciOiJKV1Qi...` |
| `Content-Type` | String | **Required** | Mime type of the request body. Must be `application/json`. | `application/json` |
| `Accept` | String | Optional | Desired format of the server response. Defaults to `application/json`. | `application/json` |

---

### Path Parameters

| Parameter | Type | Required? | Description |
| :--- | :--- | :--- | :--- |
| `project_id` | String (UUIDv4) | **Required** | The unique identifier of the target parent project. |

---

### Request Body Parameters

```json
{
  "title": "String",
  "description": "String",
  "assignee_id": "String (UUIDv4)",
  "due_date": "String (ISO 8601)",
  "priority": "String"
}
