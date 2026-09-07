# UNIBEN IT — Blockchain Learning: Assignment Submission Guide
 
Welcome! This repo is where members of the UNIBEN IT Blockchain Learning group submit their assignments. Follow the steps below to submit yours.
 
## How to Submit
 
1. **Get the repo on your machine** — pick one:
   - **Fork it**: Click the "Fork" button at the top right of this repo, then clone *your fork* to your computer.
```
     git clone https://github.com/<your-username>/<repo-name>.git
```
   - **Clone it directly** (if you have write access):
```
     git clone https://github.com/<org-or-owner>/<repo-name>.git
```
 
2. **Create your branch** (recommended, but optional if you're working on your own fork):
```
   git checkout -b <your-github-username>
```
 
3. **Create your assignment file**
   - Inside the `submissions/` folder, create a new Markdown file named after your GitHub username:
```
     submissions/<your-github-username>.md
```
     Example: if your GitHub username is `jane-doe`, create `submissions/jane-doe.md`
 
4. **Answer the assignment questions** inside that file. Use the template below so everyone's submission is easy to read and grade.
5. **Commit and push your changes**
```
   git add submissions/<your-github-username>.md
   git commit -m "Add assignment submission - <your-github-username>"
   git push origin <your-branch-name>
```
 
6. **Open a Pull Request**
   - Go to your fork (or the branch you pushed) on GitHub and open a Pull Request (PR) against the main repo's `main` branch.
   - Give your PR a clear title, e.g. `Assignment submission - <your-github-username>`.
   - Wait for review/merge.
> ⚠️ Please don't edit or delete anyone else's submission file. Only touch the file with your own username.
 
## Assignment Questions
 
Copy the template below into your `submissions/<your-github-username>.md` file and fill in your answers.
 
```markdown
# Blockchain Assignment — <your-github-username>
 
## 1. What is blockchain?
 
 
## 2. What problems does it solve?
 
 
## 3. Which industries can it be used in? (brief examples)
 
 
## 4. What is encryption?
 
 
## 5. What is a hash function?
 
 
## 6. What is on-chain?
 
 
## 7. What is a Merkle tree?
 
 
## 8. Bonus: Given a Merkle tree already built from four transactions (Ha, Hb, Hc, Hd), how would you add a fifth transaction (He) to the tree without tampering with the existing transactions?
 
```
 
## Folder Structure
 
```
.
├── README.md
└── submissions/
    ├── example-username.md
    ├── <your-github-username>.md
    └── ...
```
 
## Need Help?
 
If you get stuck on Git/GitHub steps (forking, cloning, branches, PRs), reach out in the group chat before the deadline.
 
Good luck! 🚀
 
