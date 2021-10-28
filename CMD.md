# Git
About Git

-version:
git --version

- to know read/write perm and time stamp of file  [also shows .git hidden folders when did post git init or clone]
ls -la

- to go one folder back
cd ..

- to go entirely back
cd

- to open text files 
vi notes.txt    or   vim notes.txt

- to save and close text files
ctrl+c 1/2 times and then 
:w --> save to a file
:q --> quit out of editor file
:q! --> quit out of editor without saving file
w --> move one word forward at a time in file
b --> move one word back at a time in file
:wq --> save file and quit editor
for more cmds -> https://gist.github.com/AaronPhalen/99d84494dfd36523c0de
--------------

-new repository(Convert directory as git repository): [Compulsory to have git repo, as add/commit won't work without it]
git init
git init --bare   [Sets up empty git repo usually on a server ready to be remote repo for a git using team] [you can make own git servers]

-old repository that you are joining into existing:
git clone [remote repo url]           
example: git clone https://github.com/saheer7/crypto.git      [entire repo will appear]

-to check if we are in git repository: [shows in which branch we are in]
git status

- to remove .git folder/repo
rm -Rf .git        [removes the git repo]  **Never run this when in master branch, as it deletes entire repo, logs etc permanently
rm -Rf .git .gitignore

- to show all branches of git  [branches is sort of copying and it dont affect master branch] [master is initial branch, Also need to commit before it can show any branches]
git branch           [shows * next to branch in which we are in currently]
git branch branch_name  [example: git branch test ; this creates a branch with name test] [Note: after creating branch it won't become current branch, hence need to move i.e git checkout] can use below cmd to create and move at a time]
git checkout -b branch_name [Created branch and moves into it; branches the one we are in current branch]
git branch -d branch_name [To delete branch]
git branch -m new_branch_name [To rename current branch name]

- to switch between branches or git repo
git checkout master        [git checkout repo_name]
example: git checkout other    [branch other becomes current branch]

- to turn on colors in git config
git config color.ui true

- After coding to add the changes to git [soft save before commiting]
git add     
example: git add notes.txt  [it'll changes git status from untracked to changes to be commited] [also shows status as modified if we have commited the file already and then edited it which is yet to be added]
git add .    [To add multiple files and changes at a time instead of using their file names]

- to revert/remove the changes
git rm

- to commit the changes to local git repo     [After commit git status changes to nothing to commit, working tree clean] [before commit it shows changes to be commited: new file: file_name or modified: file_name when modified]
git commit    [this will ask for a message about the commit]
git commit -m "I have added the notes file" [To commit along with a message without opening the editor]

- If any warning message/problem when using git commit saying about a name or mail address
git config --local user.name saheer  [to keep author information in commit]
git config --local user.email saheer@gmail.com [ to add mail]  ----[these credentials will be added as part of commit]

- to push the changes to remote git repo
git push

- To look back in history and see all of our commits
git log      [shows author, mail and timestamp along with the commit message]
git log --oneline  [shows all the commits in one line]

- To see immediate parent branch of current branch
git show-branch \
| sed "s/].*//" \
| grep "\*" \
| grep -v "$(git rev-parse --abbrev-ref HEAD)" \
| head -n1 \
| sed "s/^.*\[//"


-----------Merging
#When master branch did not change, branching other to master [fast forward merge]
git merge branch_name [currently being in master merging the other branch into master]

#when master branch & other branch both had changes [True merge]
git merge branch_name  [Be in current branch in which the merge should have happen]

#When in conflict stage [use when merge commit is unseccussful] [Happens when line starting is same and has difference in the next string, i.e this is first line; this is old line here conflict happens]
git merge --abort   [cancels the merge]

#when conflict merge status then can check where it happened
vi t.txt  
example output:
<<<<<<< HEAD
This is v1 line   [current branch]
=======
This is master line
>>>>>>> master_1

option 1: to edit manually in above conflict and save
- It'll show status as both modified; hence git add (here it show status as conflict fixed) and commit it
Option 2: when in conflict stage use below cmd [uses Vimdiff tool, it opens 4 windows] 
git mergetool               [to move between windows use ctrl+w and then press arrow key]
                            [1st window is current branch, 3rd branch is one we want to merge, 2nd is common ancestor i.e changes before they actually changed, 4ht is the file after we deal with conflict]
                            [ use key ]c to jumpt to next conflict; [c to jumpt to previous conflict if we have multiple conflict]
                            [:diffget or :diffg and type first 2 letters i.e LO, BA, RE which variant you want out of 3 and press enter] [:wqall cmd to write quit all]
                            [conflicts after resolved, commit to save]
git config merge.tool vimdiff    [To specify merge tool to select vimdiff use this]
Option 3: using GUI (eg: sourcetree); in file status, right clck and resolve conflict i.e by various options or launching external merge tool]

---------- Remotes & Pushing


