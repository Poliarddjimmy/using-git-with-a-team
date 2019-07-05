# using-git-with-a-team
USING GIT IN A TEAM: A CHEATSHEET
About half the time I use Git on projects only I will ever see, and the rest of the time I work collaboratively with a handful of people in my team. The workflow outlined below caters very well to this kind of use, and we've had success with it while we've been building Boords.

It's aimed at people who want to use Git in a simply, efficiently and with a minimum of fuss. I've been heavily influenced by the concepts covered in the Git course on Upcase. If you're looking to improve your skills as a developer I can heartily recommend signing up for a subscription with them.

As I say, the ideas here aren't anything new. It basically boils down to check out a new branch, work on it, then merge your changes back into the master branch in a single, curated commit. The idea is that by merging a single commit with all your changes rather than lots of smaller commits, your master branch nice stays and neat.

THE CHEATSHEET
Download as PDF

"Git workflow cheatsheet"

STEP BY STEP
To give a little more context, let's go through each of the steps above in a bit more detail so we can investigate what's going on.

STEP 1: CREATE A NEW BRANCH TO WORK ON
# Create a new feature branch
git branch jc_new_feature
# Checkout your new feature branch
git checkout jc_new_feature
When naming feature branches, a good best practice is to start with your initials, then the feature name (e.g. jc_feature_name). This helps others working on a project to see who's been doing what.

STEP 2: WRITE SOME CODE, COMMIT REGULARLY
# Add all files to the stage
git add .
# Commit files 
git commit -m "Description of this commit"
# Optional (but recommended) push local branch to remote
git push origin jc_feature_name
Commit your code regularly. I've never regretted making a commit, but have regretted not making one. You'll have a chance to change your commit messages before merging back into master.

STEP 3: FETCH WHEN YOU'RE DONE
When you're ready to merge your features back into the master branch, run git fetch.

git fetch
Fetching makes sure you're up to date when merging changes back into master. This doesn't actually merge the code with the code your machine (git pull does that), but instead updates references to any remote changes which may have happened while you've been working locally. It's groundwork for the next stage.

STEP 4: SQUASH YOUR COMMITS AND GET READY TO MERGE
Now you'll rebase your changes into the master branch. This effectively condenses down all the commits you've made on your feature branch (jc_feature_name) into one commit. We'll merge this one single commit back into the master branch, keeping everything nice and neat.

# Open the interactive rebase tool
git rebase -i origin/master
This will open an interactive rebase tool, which shows all the commits you've made on your branch. You'll then "squash" all your changes into one commit.

To do this, replace pick with s for all but the top commit. s is shorthand for squash - imagine all the changes you've made being "squashed" up into the top commit.

"Git rebase GIF"
Interactive rebase tool

"Git rebase GIF"
"Squashing" three commits into one. Here the second and third commits are squashed into the first commit.

When you close this window you'll see all your existing commits, which you can edit down into a simpler, more concise commit message.

"Git rebase GIF"
All previous commit messages

"Git rebase GIF"
Replacing existing commits with a new commit message

Exit the rebase tool and you're ready to merge.

"Git rebase GIF"

5. MERGE YOUR CHANGES
Switch to the master branch in preparation of merging your changes. When merging always remember that you're merging into the branch you're currently on.

# Checkout the master branch
git checkout master
# Merge jc_feature_name INTO master
git merge jc_feature_name
The changes from the jc_feature_name branch are now merged into your master branch. Happy days. Now's a good time to push your changes to the remote master branch.

# Push your local master branch to remote 
git push origin master
6. CLEANUP
With your changes merged into the master branch, you can safely delete your feature branches.

# Delete remote feature branch (the colon is important!)
git push origin :jc_feature_name
# Delete local branch
git branch -d jc_feature_name
And with that, you're done.

MAKING IT WORK
It's very easy to feel insecure about using Git, and the spectre of losing work looms large. The key to making this system work is to go through the process a lot, regularly branching and merging. This gets you comfortable with the workflow and has the added bonus of making sure one branch never gets too far out of line with another.

It's not a perfect system. It doesn't take into account pull requests for one. Fixing merge conflicts can be fiddly (although this is the case regardless of your workflow). But overall it gets the job done and I can say without hesitation that it's made my work, and by extension my very existence, that little bit easier
