 
 [Ask Question](https://stackoverflow.com/questions/ask)


Is there any way to use these three commands in one?

<code>git add .
git commit -a -m "commit" (do not need commit message either)
git push</code> 

Sometimes I'm changing only one letter, CSS padding or something. Still, I have to write all three commands to push the changes. There are many projects where I'm only one pusher, so this command would be awesome!





While I agree with Wayne Werner on his doubts, this is technically an option:

<code>git config alias.acp '! git commit -a -m "commit" && git push'</code> 

Which defines an alias that runs `commit` and `push`. Use it as `git acp`. Please be aware that such "shell" aliases are always run from the root of your git repository.

Another option might be to write a post-commit hook that does the push.





I ended up adding an alias to my .gitconfig file

<code>[alias]
    cmp = "!f() { git add -A && git commit -m \"$@\" && git push; }; f"

Usage: git cmp "Long commit message goes here"</code> 

Adds all files, then uses the comment for the commit message and pushes it up to origin.

I think it's a better solution because you have control over what the commit message is.


 


If the file is already being tracked then you do not need to run `git add`, you can simply write `git commit -am 'your message'`

If you do not want to write a commit message you might consider doing something like

`git commit --allow-empty-message -am ''`


I use a batch file:

```
@ECHO OFF
SET /p comment=Comment:
git add *
git commit -a -m "%comment%"
git push

```



You can try [gitu](https://www.npmjs.com/package/git-upload).

For the first time (node js has to be installed):

<code>npm install -g git-upload</code> 

After that:

<code>gitu COMMIT_MSG</code> 

To issue those three commands at once.

The good thing is that you **don't have to worry when you reinstall your system or when you want to do this on different computers and No file modification is needed.** This also **work on different platforms** (not just Linux and Mac, but also Windows) just that you have to install `npm` and `nodejs` (`git` of course).




My tip :

> git config --global alias.acpp '!git add -A && branchatu="$(git symbolic-ref HEAD 2>/dev/null)" && branchatu=${branchatu##refs/heads/} && git commit -m "$1" && shift && git pull -u origin $branchatu && git push -u origin $branchatu'

