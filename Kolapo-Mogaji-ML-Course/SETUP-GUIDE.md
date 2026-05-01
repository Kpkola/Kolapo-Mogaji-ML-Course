# How to Use This Portfolio Scaffold

This is a workflow guide. Delete this file before pushing to GitHub — it's just for you.

## What You're Working With

A complete portfolio scaffold with:
- A polished main `README.md` introducing you and listing labs/assignments
- 6 lab folders (`Labs/Lab1/` through `Labs/Lab6/`), each with a templated `README.md`
- 6 assignment folders (`Assignments/Assignment1/` through `Assignments/Assignment6/`), each with a templated `README.md`
- A `.gitignore` configured for Python/Jupyter projects
- An MIT `LICENSE` file

## Step-by-Step Workflow

### 1. Drop your code in

For each lab and assignment, copy your `.ipynb` notebook (or `.py` script, or both) into the matching folder. Example:

```
Labs/Lab1/  ←  drop your Lab 1 notebook here
Labs/Lab2/  ←  drop your Lab 2 notebook here
...
Assignments/Assignment1/  ←  drop your Assignment 1 notebook here
...
```

If your labs were named something like `Lab_KMeans.ipynb`, just rename the folder to match (e.g., `Labs/Lab1` → `Labs/Lab1-KMeans`) and update the link in the main `README.md` accordingly. Keeping the folder name human-readable looks more professional than `Lab1`.

### 2. Customize the main README

Open the top-level `README.md` and:

- **Update the lab table** — replace _"Update with your lab title"_ with your actual lab titles. Don't be vague. "K-Means Clustering on Iris Dataset" lands better than "Clustering Lab."
- **Update the assignment table** — same thing, replace the placeholders.
- **Write the Reflection paragraph** at the bottom. Three to four sentences is plenty. The prompts inside the file will guide you.

The "About Me" paragraph is already drafted using your background — read it and tweak anything that feels off.

### 3. Customize each lab README

Open each `Labs/LabN/README.md` and replace the placeholder text. The structure is:

- **What This Lab Was About** — 2–3 sentences on the lab task
- **What I Did** — 3–4 bullet points of the main steps
- **What I Learned** — 2–3 bulleted concepts, one sentence each
- **Challenges I Faced** — pick one specific thing that didn't work the first time. **Be specific.** Vague challenges read as filler.
- **How to Run** — usually no changes needed unless your lab has special setup
- **Files in This Folder** — list your actual notebook filename

You can knock out one lab README in 5–10 minutes once you remember what each lab covered.

### 4. Customize each assignment README

These are more detailed than lab READMEs. Same drill but with extra sections:

- **The Problem** — set up the problem clearly, 2–4 sentences
- **My Approach** — what method, why this method, key decisions made along the way
- **Implementation** — bullet walkthrough of what the code does
- **Results** — actual numbers in the table, or a screenshot
- **What the Results Mean** — most important section, where you show you can interpret results, not just produce them
- **Limitations and Future Work** — optional but strong

Plan on 10–15 minutes per assignment README.

### 5. Initialize the Git repo and push

Open a terminal in this folder and run:

```bash
git init
git add .
git commit -m "Initial commit — ML course portfolio"
git branch -M main
```

Then go to **github.com/new**, create a new repository named `Kolapo-Mogaji-ML-Course`, **make it public**, and **don't** initialize with README/license/gitignore (this scaffold already has them).

After creating, GitHub gives you a URL. Run:

```bash
git remote add origin https://github.com/Kpkola/Kolapo-Mogaji-ML-Course.git
git push -u origin main
```

(Replace the URL with whatever GitHub shows you. You'll need a Personal Access Token for the password — same drill as your Glucose Guardian repo. Get one at github.com/settings/tokens.)

### 6. Verify in incognito

Open the repo URL in an incognito browser window. If it loads without asking you to sign in, the repo is public — exactly what the rubric requires.

### 7. Submit

Open the Word doc (`Submission.docx` if I built it for you) and confirm the GitHub URL is correct. Submit that one-page Word doc.

## A Small Note on the Rubric

The course doesn't grade your code. They grade:
- Repository organization (this scaffold handles it)
- README quality (your job)
- Professional presentation (this scaffold handles it; your tone in the READMEs handles the rest)

So the part that determines your grade is the time you put into writing the lab and assignment READMEs. Don't rush those. They're the whole assignment.

---

When you're done, delete this `SETUP-GUIDE.md` file before pushing to GitHub. It's not part of the deliverable.
