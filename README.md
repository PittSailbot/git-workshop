# Git Workshop

This workshop will walk you through how to contribute to a shared repository. By the end of this workshop you will know how to:
- commit and push changes
- create branches
- create pull requests
- handle merges and conflicts


## Workshop Flow

1. Install Git and create a GitHub account.
2. Download and install VS Code.
3. Clone the workshop repo.
4. Create a branch.
5. Add a new `.txt` file.
6. Commit & push that change.
7. Open a pull request into `main`.
8. Make a change to a shared `.txt` file.
9. Handle a merge conflict.

## 1. Install Git & Create A GitHub Account

Git is the tool that tracks your project history and lets you collaborate with other people without overwriting each other's work.

1. Download and install Git from https://git-scm.com/downloads.
2. Create a GitHub account at https://github.com/signup if you do not already have one.
3. Paste your GitHub username in the #controls-team discord so I can add you to the PittSailbot organization

## 2. Download VS Code

VS Code is the editor we will use for this workshop.

1. Download and install VS Code from https://code.visualstudio.com/download.
2. Open VS Code once the install is complete so it can finish initial setup.

## 3. Clone The Workshop Repo

Now get the workshop code onto your machine.

1. Open our repo online https://github.com/PittSailbot/git-workshop
2. Click the green `<> Code` button and copy the link under HTTPS
3. In VS Code, open the Command Palette with Ctrl+Shift+P.
4. Enter `Git: Clone`.
5. Paste the repo URL you copied.
6. Choose a local folder where you want the repo to live.
7. Open the cloned folder when VS Code finishes.

You can also clone from a terminal if you prefer:

```bash
cd "C:/<your>/<install>/<location of choice>/"
git clone https://github.com/PittSailbot/git-workshop.git
```

## 4. Make A Branch

Branches give you your own virtual sandbox to work in. This lets you work on a change without others impacting your work. 

1. Open a terminal in the cloned repository using `Ctrl + \``.
2. Create a new branch using your name:

```bash
git checkout -b your-name
```

Note: If git asked you to login with your GitHub username and a _token_, follow [this guide](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens#creating-a-fine-grained-personal-access-token) to make an authentication token.

1. Confirm you are on the new branch:

```bash
git branch
```

The branch with the `*` is the one you are currently on.

## 5. Add A New `.txt` File

1. Right-click the `hello` folder and create a new file with `your-name.txt`
2. Add a fun fact about yourself, the strongest animal your think you can beat up or any other lines of text you want to the file.
3. Save the file.
4. Check `git status` to confirm Git sees the new file:

```bash
git status
```

You should see the file listed under Untracked. This means that git is not currently monitoring changes to your file. 

## 6. Commit The Change

A commit is a saved snapshot of your work. It's like hitting "Save" on a word document except a bit more intentional. Each commit comes with a message where you can explain what and why you changed something. It's good to commit whenever you've done a discrete, meaningful amount of work. 

1. Stage the file:

```bash
git add hello/your-name.txt
```

2. Create a commit with a clear message:

```bash
git commit -m "Add my first workshop file"
```

Now, if you open the source control panel on the left-side of VSCode, you can see the graph containing your commit. Commiting only saves your work. It does not publish it to others. This can be useful when you are testing new features since you can control git's history and combine, reorder and rework commits before they are published.

## 7. Push The Change

Now that we've commited our new file, pushing will publish our commit to GitHub.

1. Push your branch to the remote repository:

```bash
git push -u origin your-name
```

2. Open the repository on GitHub and confirm your branch appears.

The `-u` flag sets the upstream branch so future pushes can use plain `git push`.

## 8. Open A Pull Request Into `main`

Pull requests are how you ask for your branch to be merged back into the `main`.

1. Go to the repository on GitHub.
2. Find and click on your branch under the branches tab.
3. Click `Compare & pull request`
4. Write a short title and summary describing your change.
5. Create the pull request.

Automatically, Github will check if there are any conflicts before you can merge. Since we only added a new file, this should be green. Go ahead and click `Merge pull request` to complete your change.

Go back to the main branch and you should be able to see your change merged into the rest of the codebase.

## 9. Make A Change To `shared.txt`

Now we will create a situation where multiple people collaborate on the same file.

1. Checkout the `McD` branch:

```bash
git checkout McD
```

2. Add something you'd like to order from McDonalds to `shared.txt`.
3. Commit and push this to the branch the same way you did before.
4. Make a pull request and merge your commit into the `main` branch.

5. Now checkout the `grocery` branch:

```bash
git checkout grocery
```

You'll see that the changes you made in the McD branch are not reflected here. This is because each branch tracks its own independent history. Until you decided to merge both branches, your changes will remain only the branch you committed to.

5. Similarly, add something you'd like to order from the grocery store to `shared.txt`
6. Commit, push and make a pull request into `main` the same way you did before.

Now, you'll see that the pull request cannot be merged automatically. This is a merge conflict.

## 10. Handle Merge Conflicts

Merge conflicts happen when Git cannot safely combine two changes on its own. In this case, you have to choose which changes you want to keep. Let's combine our two lists on main. 

1. In VSCode, enter `git merge origin/grocery` from the `main` branch. This will pull in the changes from the grocery branch into the main branch.
2. Git should report a conflict in the file `shared.txt`.
3. Open the file and look for conflict markers like these:

```text
<<<<<<< HEAD
your change
=======
their change
>>>>>>> other-branch
```

4. Click `Accept Both Changes` and move the items into their respective lists
5. Mark the file as resolved and finish the merge:

```bash
git add shared.txt
git commit
```

8. Push the resolved branch if needed.

## Key Ideas To Reinforce

* Git tracks history locally and GitHub stores a shared copy online.
* Branches let people work independently until the changes are ready to combine.
* Commits should represent one meaningful change.
* Pull requests are the review and merge point for shared work.
* Merge conflicts are normal and usually mean two people changed the same part of a file.

## Extras
- [Cheat Sheet](https://git-scm.com/cheat-sheet)
  - `git stash` lets you save your changes without commiting

### Oh Sh*t! Where's the undo?
Sometimes mistakes happen when working with git. You might forget to include a file or change in your commit. 

I forgot to include something in my commit:
- Stage your additional changes and run `git commit --ammend`. This lets you tack on those changes into your last commit. Git will open a file containing your last commit message. You can edit the message and then close the file to finish the ammend.

I didn't mean to commit that:
- If you want to delete the commit like it never existed, use `git drop`. Note that these changes will be gone.
- If you want to rework the commit, use `git undo`. The changes made in the commit will be restored in your workspace while deleting the commit from history.

I don't know what happened. I want to nuke everything:
- `git reset` will revert your local changes to a specific commit or branch.
  - using the flag soft `git reset --soft` will keep your uncommitted changes 
    - `git reset --soft HEAD~~1` will go back 1 commit
  - using the flag hard `git reset --hard` will DELETE any uncommitted changes you have