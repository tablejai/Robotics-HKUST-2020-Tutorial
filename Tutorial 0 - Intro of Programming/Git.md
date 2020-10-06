Authored by: Nicholas Christanto
Contact: nchristanto@connect.ust.hk

# Git 2020
## Git
Git is a command line tool that will help us with version control in several different ways:
- Allowing us to keep track of changes we make to our code by saving snapshots of our code at a given point in time.
- Allowing us to easily synchronize code between different people working on the same project by allowing multiple people to pull information from and push information to a repository stored on the web.
- Allowing us to make changes to and test out code on a different branch without altering our main code base, and then merging the two together.
- Allowing us to revert back to earlier versions of our code if we realize we’ve made a mistake.
## Repository
A Git repository is a file location where we’ll store all of the files related to a given project. These can either be remote (stored online) or local (stored on your computer).

## GitHub
GitHub is a website that allows us to store Git repositories remotely on the web.
1. Make sure you have a GitHub Account
1. Click __+__ in the top right of the web and click on "New Repository"
1. Write the name of the repository.
1. _Optional_ Write description and/or add ReadMe.md to your repository.

### How to use GitHub
Clone your repository to your local computer
- make sure you have git installed in your computer by typing __git__ in the terminal.
- To move around in terminal, you can use **cd _name**
- You would want to create a designated directory in your computer for cloning using **mkdir _name of your repository_**.
- To clone the repository, type __git clone 'url'__ (url of your repository)

You can now create files and save it in that directory.

### Add
- After creating the files filled with codes, you can go to the terminal and into the cloned repository.
- Now, to let Git know that it should be keeping track of the new file you’ve made, Run **git add <new file name>** to track that specific file, or git add . to track all files within that directory.

### Commit
- After making some changes to a file, we can commit those changes. To do this, we run: **git commit -m "some message"** where the message describes the changes you just made.
- Run **git status** to see how our code compares to the code on the remote repository
- When we’re ready to publish our local commits to Github, we can run **git push**. 
- If you’ve only changed existing files and not created new ones, we can condense this into one command: **git commit -am "some message"**. 
- Use **git log** to see a history of all of your commits on that repository.

[Git Reference](https://cs50.harvard.edu/web/2020/notes/1/#:~:text=GitHub%20is%20a%20website%20that%20allows%20us%20to%20store%20Git%20repositories%20remotely%20on%20the%20web.)
[.gitigonre Reference](https://www.pluralsight.com/guides/how-to-use-gitignore-file)
