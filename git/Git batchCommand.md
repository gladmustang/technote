 
 [Ask Question](https://stackoverflow.com/questions/ask)


Is there any way to use these three commands in one?

<code>git add .
git commit -a -m "commit" (do not need commit message either)
git push</code> 

Sometimes I'm changing only one letter, CSS padding or something. Still, I have to write all three commands to push the changes. There are many projects where I'm only one pusher, so this command would be awesome!


 [edited May 22 '14 at 6:41](https://stackoverflow.com/posts/19595067/revisions "show all edits to this post")

 ![](https://i.stack.imgur.com/xEJu4.jpg?s=32&g=1)

 [alex](https://stackoverflow.com/users/31671/alex)
 291k144695853

 | 

 asked Oct 25 '13 at 16:31

 ![](https://i.stack.imgur.com/BQRsF.jpg?s=32&g=1)

 [Gediminas](https://stackoverflow.com/users/1412149/gediminas)
 1,75841830


 Have you tried writing a shell script? – [Paul](https://stackoverflow.com/users/103081/paul "13,048 reputation") [Oct 25 '13 at 16:34](https://stackoverflow.com/questions/19595067/git-add-commit-and-push-commands-in-one#comment29083965_19595067)


 You don't need a commit message? [No](http://i.imgur.com/a9IAGPv.jpg). Also, `-a` means `add .`, so there's one down. – [Wayne Werner](https://stackoverflow.com/users/344286/wayne-werner "22,276 reputation")[Oct 25 '13 at 16:35](https://stackoverflow.com/questions/19595067/git-add-commit-and-push-commands-in-one#comment29084009_19595067)


 [stackoverflow.com/questions/7852148/…](http://stackoverflow.com/questions/7852148/function-in-bash-to-commit-and-push-in-one-command "function in bash to commit and push in one command") – [CodeGroover](https://stackoverflow.com/users/324098/codegroover "1,786 reputation") [Oct 25 '13 at 16:38](https://stackoverflow.com/questions/19595067/git-add-commit-and-push-commands-in-one#comment29084088_19595067)

 |
| 

| 8 |   |

 | 
 @WayneWerner add . and commit -a are different – [CodeGroover](https://stackoverflow.com/users/324098/codegroover "1,786 reputation") [Oct 25 '13 at 16:39](https://stackoverflow.com/questions/19595067/git-add-commit-and-push-commands-in-one#comment29084116_19595067)

 |
| 

| 2 |   |

 | 
 "(do not need commit message either)" [images.wikia.com/dragonball/images/a/a7/Facepalm_227785.jpg](http://images.wikia.com/dragonball/images/a/a7/Facepalm_227785.jpg) – [Ajedi32](https://stackoverflow.com/users/1157054/ajedi32 "18,413 reputation") [Oct 25 '13 at 20:12](https://stackoverflow.com/questions/19595067/git-add-commit-and-push-commands-in-one#comment29090335_19595067)

 |

 [show **2** more comments](https://stackoverflow.com/questions/19595067/git-add-commit-and-push-commands-in-one "expand to show all comments on this post")

 |

 <a name="tab-top"></a>

## 14 Answers

 [active](https://stackoverflow.com/questions/19595067/git-add-commit-and-push-commands-in-one?answertab=active#tab-top "Answers with the latest activity first")[oldest](https://stackoverflow.com/questions/19595067/git-add-commit-and-push-commands-in-one?answertab=oldest#tab-top "Answers in the order they were provided")[votes](https://stackoverflow.com/questions/19595067/git-add-commit-and-push-commands-in-one?answertab=votes#tab-top "Answers with the highest score first")

<a name="23328996"></a>

| 
 <a class="vote-up-off" title="This answer is useful">up vote</a>110<a class="vote-down-off" title="This answer is not useful">down vote</a>

 | 

Building off of @Gavin's answer:

Making lazygit a function instead of an alias allows you to pass it an argument. I have added the following to my .bashrc (or .bash_profile if Mac):

<code>function lazygit() {
    git add .
    git commit -a -m "$1"
    git push
}</code> 

This allows you to provide a commit message, such as

<code>lazygit "My commit msg"</code> 

You could of course beef this up even more by accepting even more arguments, such as which remote place to push to, or which branch.

| 
 [share](https://stackoverflow.com/a/23328996 "short permalink to this answer")[improve this answer](https://stackoverflow.com/posts/23328996/edit)

 | 

 answered Apr 27 '14 at 21:06

 ![](https://i.stack.imgur.com/paVAq.jpg?s=32&g=1)

 [btse](https://stackoverflow.com/users/931938/btse)
 4,53621723

 |

 |
|   | 

| 

| 1 |   |

 | 
 @JoeYahchouchi Not working how? Have you reset your terminal (or resourced the bashrc file)? What happens if you type `which lazygit`? – [btse](https://stackoverflow.com/users/931938/btse "4,536 reputation") [Mar 21 '15 at 19:31](https://stackoverflow.com/questions/19595067/git-add-commit-and-push-commands-in-one#comment46589168_23328996)

 |
| 

| 2 |   |

 | 
 Restart not needed, just do "source .bashrc" – [Sambit Tripathy](https://stackoverflow.com/users/1282935/sambit-tripathy "311 reputation") [May 14 '15 at 19:09](https://stackoverflow.com/questions/19595067/git-add-commit-and-push-commands-in-one#comment48591720_23328996)

 |
| 

| 13 |   |

 | 
 could use `$*` instead of `$1` to save typing the quotes: `lazygit My commit msg` – [Kai Carver](https://stackoverflow.com/users/153144/kai-carver "1,331 reputation") [Nov 5 '15 at 22:04](https://stackoverflow.com/questions/19595067/git-add-commit-and-push-commands-in-one#comment54891109_23328996)

 |
| 

| 7 |   |

 | 
 @KaiCarver Nice thought, but personally I do not like it. It prevents you from using multiple args, and also goes against the normal convention of a single string arg with spaces being wrapped in quotes. This is second nature to me at this point (and I would assume a lot of developers). Leaving out the quotes feels dirty. – [btse](https://stackoverflow.com/users/931938/btse "4,536 reputation") [Nov 5 '15 at 22:29](https://stackoverflow.com/questions/19595067/git-add-commit-and-push-commands-in-one#comment54891797_23328996)

 |
| 

| 3 |   |

 | 
 lazygit, best name ever! – [user1447414](https://stackoverflow.com/users/1447414/user1447414 "461 reputation") [Apr 18 '16 at 11:50](https://stackoverflow.com/questions/19595067/git-add-commit-and-push-commands-in-one#comment60974457_23328996)

 |

 [show **4** more comments](https://stackoverflow.com/questions/19595067/git-add-commit-and-push-commands-in-one "expand to show all comments on this post")

 |

 [![](https://s.zkcdn.net/Advertisers/054331674d33424abacccb7e6fa6956e.png)](https://engine.adzerk.net/r?e=eyJhdiI6NDE0LCJhdCI6NCwiYnQiOjAsImNtIjo0NzE0OTMsImNoIjoxMTc4LCJjayI6e30sImNyIjoxNjM4OTkxLCJkaSI6IjFiZGY1OTIyOGFjZjQ1YzdiOGU3NTQ1MTU0M2E3NzMwIiwiZG0iOjEsImZjIjoxOTQzNDQ1LCJmbCI6MjE0MjMxMiwiaXAiOiI0OS42Ni40Mi4xNDgiLCJrdyI6ImdpdCIsIm53IjoyMiwicGMiOjAsImVjIjowLCJwciI6MTYwNCwicnQiOjEsInJmIjoiaHR0cHM6Ly93d3cudjJleC5jb20vdC8yMzg5NjEiLCJzYSI6IjMiLCJzYiI6ImktMGFkZWI1NGIyZjg2YzAzMTEiLCJzcCI6MzA1NzMsInN0Ijo4Mjc3LCJ1ayI6InVlMS0zNWE4NDIxNmIzMmY0ODg3OTYyN2Y4OGE4ODAwZjYzYyIsInpuIjo0NCwidHMiOjE0OTk1MzU2NzE1ODAsImJmIjp0cnVlLCJwbiI6ImFkemVyazQ1MDgzMjkzNSIsInVyIjoiaHR0cDovL3N0YWNrb3ZlcmZsb3cuY29tL2pvYnM_dXRtX3NvdXJjZT13ZWJzaXRlJnV0bV9tZWRpdW09YmFubmVyJnV0bV9jb250ZW50PWxlYWRlcmJvYXJkXzkmdXRtX2NhbXBhaWduPWhvdXNlX2Fkc19ob3VzZV9hZHNfUk9TX1NPIn0&s=Le0lunay-G6KdBlEC8A9y58RPMw)![](https://engine.adzerk.net/i.gif?e=eyJhdiI6NDE0LCJhdCI6NCwiYnQiOjAsImNtIjo0NzE0OTMsImNoIjoxMTc4LCJjayI6e30sImNyIjoxNjM4OTkxLCJkaSI6IjFiZGY1OTIyOGFjZjQ1YzdiOGU3NTQ1MTU0M2E3NzMwIiwiZG0iOjEsImZjIjoxOTQzNDQ1LCJmbCI6MjE0MjMxMiwiaXAiOiI0OS42Ni40Mi4xNDgiLCJrdyI6ImdpdCIsIm53IjoyMiwicGMiOjAsImVjIjowLCJwciI6MTYwNCwicnQiOjEsInJmIjoiaHR0cHM6Ly93d3cudjJleC5jb20vdC8yMzg5NjEiLCJzYSI6IjMiLCJzYiI6ImktMGFkZWI1NGIyZjg2YzAzMTEiLCJzcCI6MzA1NzMsInN0Ijo4Mjc3LCJ1ayI6InVlMS0zNWE4NDIxNmIzMmY0ODg3OTYyN2Y4OGE4ODAwZjYzYyIsInpuIjo0NCwidHMiOjE0OTk1MzU2NzE1ODEsImJmIjp0cnVlLCJwbiI6ImFkemVyazQ1MDgzMjkzNSIsImZxIjowfQ&s=Kqgd2daRPJbRVukn-7EoqwvGzio)

<a name="19595658"></a>

| 
 <a class="vote-up-off" title="This answer is useful">up vote</a>29<a class="vote-down-off" title="This answer is not useful">down vote</a>

 | 

While I agree with Wayne Werner on his doubts, this is technically an option:

<code>git config alias.acp '! git commit -a -m "commit" && git push'</code> 

Which defines an alias that runs `commit` and `push`. Use it as `git acp`. Please be aware that such "shell" aliases are always run from the root of your git repository.

Another option might be to write a post-commit hook that does the push.

| 
 [share](https://stackoverflow.com/a/19595658 "short permalink to this answer")[improve this answer](https://stackoverflow.com/posts/19595658/edit)

 | 

 answered Oct 25 '13 at 17:06

 ![](https://www.gravatar.com/avatar/94d7f9208e421fe3fcdb2953ede58280?s=32&d=identicon&r=PG)

 [Tilman Vogel](https://stackoverflow.com/users/119725/tilman-vogel)
 4,47232325

 |

 |
|   | 

| 

|    |   |

 | 
 @wlz I just tried it and it works fine. Note that the whole string is inside single-quotes. `git` automatically added the escapes (checked with `git config -e`). – [Tilman Vogel](https://stackoverflow.com/users/119725/tilman-vogel "4,472 reputation") [Feb 10 '14 at 17:26](https://stackoverflow.com/questions/19595067/git-add-commit-and-push-commands-in-one#comment32780105_19595658)

 |
| 

|    |   |

 | 
 Sorry , you're right :) . I directly edit the .gitconfig file . The " has already escaped with \" . – [wlz](https://stackoverflow.com/users/1677000/wlz "128 reputation") [Feb 12 '14 at 1:02](https://stackoverflow.com/questions/19595067/git-add-commit-and-push-commands-in-one#comment32838984_19595658)

 |
| 

|    |   |

 | 
 This is definitely cool. – [Evan Hu](https://stackoverflow.com/users/906945/evan-hu "550 reputation") [Jun 28 '15 at 13:18](https://stackoverflow.com/questions/19595067/git-add-commit-and-push-commands-in-one#comment50215765_19595658)

 |
| 

|    |   |

 | 
 Why isn't this the accepted answer? It does what was asked. +1. – [user1712447](https://stackoverflow.com/users/1712447/user1712447 "56 reputation") [May 9 at 20:47](https://stackoverflow.com/questions/19595067/git-add-commit-and-push-commands-in-one#comment74794175_19595658)

 |

 <a class="js-add-link comments-link disabled-link " title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”.">add a comment</a>

 |

<a name="19595298"></a>

| 
 <a class="vote-up-off" title="This answer is useful">up vote</a>24<a class="vote-down-off" title="This answer is not useful">down vote</a>

 | 

I think you might misunderstand the workflow that git was designed for. (To clarify/correct what I meant in the comment, you don't need the `git add .`, since `commit -a` usually serves the same purpose - adding any changes that have not yet been staged, if the files have already been added)

Typically you'll do something like this:

<code># make some changes
$ git commit -a -m "Changed something"
# make some more changes
$ git commit -a -m "Changed something else"</code> 

wash, rinse, repeat, until you've finished feature X, or you're at a stopping point, or you just want other people to see what you've done. Then you do

<code>$ git push</code> 

Git is not SVN - but it appears that you're trying to use it as such. You might find some of the resources at the end of the article [here](http://www.ibm.com/developerworks/library/l-git-subversion-1/) to be of some use.

| 
 [share](https://stackoverflow.com/a/19595298 "short permalink to this answer")[improve this answer](https://stackoverflow.com/posts/19595298/edit)

 | 

 [edited Oct 25 '13 at 21:19](https://stackoverflow.com/posts/19595298/revisions "show all edits to this post")

 | 

 answered Oct 25 '13 at 16:44

 ![](https://www.gravatar.com/avatar/3827b2facd01ed6a64a96df00d4b877a?s=32&d=identicon&r=PG)

 [Wayne Werner](https://stackoverflow.com/users/344286/wayne-werner)
 22.3k1085161

 |

 |
|   | 

| 

| 4 |   |

 | 
 +1 for the explanation about the workflow. However `git add .` and `git commit -a` [are not the same thing](http://stackoverflow.com/questions/3541647/git-add-vs-git-commit-a) – [Gabriele Petronella](https://stackoverflow.com/users/846273/gabriele-petronella "79,315 reputation") [Oct 25 '13 at 16:46](https://stackoverflow.com/questions/19595067/git-add-commit-and-push-commands-in-one#comment29084346_19595298)

 |
| 

|    |   |

 | 
 If I'm deleting/creating a file. Does `git commit -a` finds it? For me it fails, but maybe something wrong has been done – [Gediminas](https://stackoverflow.com/users/1412149/gediminas "1,758 reputation") [Oct 25 '13 at 16:50](https://stackoverflow.com/questions/19595067/git-add-commit-and-push-commands-in-one#comment29084460_19595298)

 |
| 

| 3 |   |

 | 
 Thanks for the explanation, but GIT will not collapse if there will be a command like this for those who knows what they are doing... – [Gediminas](https://stackoverflow.com/users/1412149/gediminas "1,758 reputation") [Oct 25 '13 at 16:55](https://stackoverflow.com/questions/19595067/git-add-commit-and-push-commands-in-one#comment29084588_19595298)

 |
| 

| 4 |   |

 | 
 @Lucas: Experienced programmers will tell you that people who ask for an automatic commit-push command don't know what they're doing. There's a reason for the 3-stage code checkin (if you're using feature branches, 4-stage). – [slebetman](https://stackoverflow.com/users/167735/slebetman "53,470 reputation") [Oct 27 '13 at 1:01](https://stackoverflow.com/questions/19595067/git-add-commit-and-push-commands-in-one#comment29115325_19595298)

 |
| 

| 1 |   |

 | 
 @slebetman: I didn't explain it correctly. With facebook apps, every single change must be deployed to live server even for development. So, we have setup commit hooks to do that. You do a change, commit it and see the change in your app. With git, I need to add, stage then push it to see a single change. Doesn't it look a overkill? – [SenG](https://stackoverflow.com/users/959939/seng "371 reputation") [May 10 '14 at 3:17](https://stackoverflow.com/questions/19595067/git-add-commit-and-push-commands-in-one#comment36182830_19595298)

 |

 [show **6** more comments](https://stackoverflow.com/questions/19595067/git-add-commit-and-push-commands-in-one "expand to show all comments on this post")

 |

<a name="35049625"></a>

| 
 <a class="vote-up-off" title="This answer is useful">up vote</a>15<a class="vote-down-off" title="This answer is not useful">down vote</a>

 | 

I ended up adding an alias to my .gitconfig file

<code>[alias]
    cmp = "!f() { git add -A && git commit -m \"$@\" && git push; }; f"

Usage: git cmp "Long commit message goes here"</code> 

Adds all files, then uses the comment for the commit message and pushes it up to origin.

I think it's a better solution because you have control over what the commit message is.

| 
 [share](https://stackoverflow.com/a/35049625 "short permalink to this answer")[improve this answer](https://stackoverflow.com/posts/35049625/edit)

 | 

 answered Jan 27 '16 at 22:48

 ![](https://www.gravatar.com/avatar/2fbfb35f1ba1c6e720bfb3ea76e3a02e?s=32&d=identicon&r=PG)

 [madcapacity](https://stackoverflow.com/users/2852690/madcapacity)
 16112

 |

 |
|   | 

| 

| 4 |   |

 | 
 this should be the best answer! – [Demonbane](https://stackoverflow.com/users/2394118/demonbane "89 reputation") [Jun 30 '16 at 13:35](https://stackoverflow.com/questions/19595067/git-add-commit-and-push-commands-in-one#comment63680628_35049625)

 |

 <a class="js-add-link comments-link disabled-link " title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”.">add a comment</a>

 |

<a name="34569930"></a>

| 
 <a class="vote-up-off" title="This answer is useful">up vote</a>13<a class="vote-down-off" title="This answer is not useful">down vote</a>

 | 

I use this on my .bash_profile

<code>gitpush() {
    git add .
    git commit -m "$*"
    git push
}
alias gp=gitpush</code> 

It executes like

<code>gp A really long commit message</code> 

Don't forget to run `source ~/.bash_profile` after saving the alias.

| 
 [share](https://stackoverflow.com/a/34569930 "short permalink to this answer")[improve this answer](https://stackoverflow.com/posts/34569930/edit)

 | 

 answered Jan 2 '16 at 19:39

 ![](https://i.stack.imgur.com/K18X5.png?s=32&g=1)

 [Rajender Joshi](https://stackoverflow.com/users/1973411/rajender-joshi)
 2,69011129

 |

 |
|   | 

| 

|    |   |

 | 
 I really like this. ...and have therefore adopted it into my own ~/.bash_profile ;) thanks.. +1 – [0x616f](https://stackoverflow.com/users/792700/0x616f "1,013 reputation") [Apr 18 at 15:54](https://stackoverflow.com/questions/19595067/git-add-commit-and-push-commands-in-one#comment74009083_34569930)

 |

 <a class="js-add-link comments-link disabled-link " title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”.">add a comment</a>

 |

<a name="21975327"></a>

| 
 <a class="vote-up-off" title="This answer is useful">up vote</a>12<a class="vote-down-off" title="This answer is not useful">down vote</a>

 | 

Set as an alias in bash:

<code>$ alias lazygit="git add .; git commit -a -m '...'; git push;";</code> 

Call it:

<code>$ lazygit</code> 

(To make this alias permanent, you'd have to include it in your .bashrc or .bash_profile)

| 
 [share](https://stackoverflow.com/a/21975327 "short permalink to this answer")[improve this answer](https://stackoverflow.com/posts/21975327/edit)

 | 

 [edited Mar 22 '14 at 2:47](https://stackoverflow.com/posts/21975327/revisions "show all edits to this post")

 | 

 answered Feb 23 '14 at 22:10

 ![](https://www.gravatar.com/avatar/18511faa3a462ee1879b242295d22a64?s=32&d=identicon&r=PG)

 [Gavin](https://stackoverflow.com/users/2980938/gavin)
 3,025165

 |

 |
|   | 

| 

|    |   |

 | 
 does it work after restart? – [Gediminas](https://stackoverflow.com/users/1412149/gediminas "1,758 reputation") [Mar 4 '14 at 11:05](https://stackoverflow.com/questions/19595067/git-add-commit-and-push-commands-in-one#comment33647450_21975327)

 |
| 

|    |   |

 | 
 > nope, it doesn't – [Gediminas](https://stackoverflow.com/users/1412149/gediminas "1,758 reputation") [Mar 9 '14 at 8:07](https://stackoverflow.com/questions/19595067/git-add-commit-and-push-commands-in-one#comment33845839_21975327)

 |
| 

|    |   |

 | 
 You would need it add that alias to .bashrc or .bash_profile to make it permanent – [Gavin](https://stackoverflow.com/users/2980938/gavin "3,025 reputation") [Mar 22 '14 at 2:46](https://stackoverflow.com/questions/19595067/git-add-commit-and-push-commands-in-one#comment34360553_21975327)

 |
| 

|    |   |

 | 
 How to do this? Thanks! – [Gediminas](https://stackoverflow.com/users/1412149/gediminas "1,758 reputation") [Mar 25 '14 at 11:36](https://stackoverflow.com/questions/19595067/git-add-commit-and-push-commands-in-one#comment34468301_21975327)

 |
| 

|    |   |

 | 
 I think this page can help to explain: [serverfault.com/questions/3743/…](http://serverfault.com/questions/3743/what-useful-things-can-one-add-to-ones-bashrc "what useful things can one add to ones bashrc") – [Gavin](https://stackoverflow.com/users/2980938/gavin "3,025 reputation") [Mar 27 '14 at 1:13](https://stackoverflow.com/questions/19595067/git-add-commit-and-push-commands-in-one#comment34545231_21975327)

 |

 <a class="js-add-link comments-link disabled-link " title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”.">add a comment</a>

 |

<a name="27631408"></a>

| 
 <a class="vote-up-off" title="This answer is useful">up vote</a>10<a class="vote-down-off" title="This answer is not useful">down vote</a>

 | 

You can use bash script , set alias to launch any command or group of commands

<code>git commit -am "your message" && git push</code> 

| 
 [share](https://stackoverflow.com/a/27631408 "short permalink to this answer")[improve this answer](https://stackoverflow.com/posts/27631408/edit)

 | 

 [edited Jun 7 at 8:45](https://stackoverflow.com/posts/27631408/revisions "show all edits to this post")

 ![](https://i.stack.imgur.com/x93aw.jpg?s=32&g=1)

 [wonea](https://stackoverflow.com/users/271200/wonea)
 1,9431254110

 | 

 answered Dec 24 '14 at 4:18

 ![](https://www.gravatar.com/avatar/71797fe963333d41de913eb798916eae?s=32&d=identicon&r=PG)

 [vuhung3990](https://stackoverflow.com/users/2939690/vuhung3990)
 3,06512030

 |

 |
|   | 

| 

| 2 |   |

 | 
 If you wish to make this an answer, please add more commentary around how it works. Answers which are simply a code dump are generally not well received. See [How to Answer](https://stackoverflow.com/questions/how-to-answer). – [Mike McCaughan](https://stackoverflow.com/users/215552/mike-mccaughan "5,437 reputation") [Dec 24 '14 at 5:01](https://stackoverflow.com/questions/19595067/git-add-commit-and-push-commands-in-one#comment43683714_27631408)

 |
| 

| 1 |   |

 | 
 sorry sir, i will update my answer – [vuhung3990](https://stackoverflow.com/users/2939690/vuhung3990 "3,065 reputation") [Dec 24 '14 at 7:05](https://stackoverflow.com/questions/19595067/git-add-commit-and-push-commands-in-one#comment43685677_27631408)

 |
| 

|    |   |

 | 
 I think this should be the correct answer. As it answer the question as succinctly as possible. Just type it into terminal and it works! If you doesn't want to add an alias an alternative would be to simply create a textExpander expand and trigger it via a key-combo. – [GitSync](https://stackoverflow.com/users/5389500/gitsync "727 reputation") [Dec 14 '16 at 15:43](https://stackoverflow.com/questions/19595067/git-add-commit-and-push-commands-in-one#comment69495488_27631408)

 |
| 

|    |   |

 | 
 this is so simple and works great, best answer! – [Sebastian](https://stackoverflow.com/users/3361975/sebastian "558 reputation") [May 15 at 21:42](https://stackoverflow.com/questions/19595067/git-add-commit-and-push-commands-in-one#comment75007702_27631408)

 |

 <a class="js-add-link comments-link disabled-link " title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”.">add a comment</a>

 |

<a name="19613173"></a>

| 
 <a class="vote-up-off" title="This answer is useful">up vote</a>6<a class="vote-down-off" title="This answer is not useful">down vote</a>

 | 

If the file is already being tracked then you do not need to run `git add`, you can simply write `git commit -am 'your message'`

If you do not want to write a commit message you might consider doing something like

`git commit --allow-empty-message -am ''`

| 
 [share](https://stackoverflow.com/a/19613173 "short permalink to this answer")[improve this answer](https://stackoverflow.com/posts/19613173/edit)

 | 

 answered Oct 26 '13 at 23:48

 ![](https://www.gravatar.com/avatar/6cc08b08f48b79df45c180b999ad250c?s=32&d=identicon&r=PG)

 [Peter Foti](https://stackoverflow.com/users/1672804/peter-foti)
 4,49632137

 |

 |
|   | 
 <a class="js-add-link comments-link disabled-link " title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”.">add a comment</a>

 |

<a name="36337403"></a>

| 
 <a class="vote-up-off" title="This answer is useful">up vote</a>2<a class="vote-down-off" title="This answer is not useful">down vote</a>

 | 

I use a batch file:

<code>@ECHO OFF
SET /p comment=Comment:
git add *
git commit -a -m "%comment%"
git push</code> 

| 
 [share](https://stackoverflow.com/a/36337403 "short permalink to this answer")[improve this answer](https://stackoverflow.com/posts/36337403/edit)

 | 

 answered Mar 31 '16 at 15:16

 ![](https://i.stack.imgur.com/UDT6m.png?s=32&g=1)

 [Márcio Souza Júnior](https://stackoverflow.com/users/2083581/m%c3%a1rcio-souza-j%c3%banior)
 412311

 |

 |
|   | 

| 

|    |   |

 | 
 probs would be easier if you accepted in args from the command line. i simply go "lezygit MESSAGE" etc. its pretty cool! – [John Hon](https://stackoverflow.com/users/5847286/john-hon "115 reputation") [Apr 20 at 3:58](https://stackoverflow.com/questions/19595067/git-add-commit-and-push-commands-in-one#comment74074118_36337403)

 |

 <a class="js-add-link comments-link disabled-link " title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”.">add a comment</a>

 |

<a name="41366192"></a>

| 
 <a class="vote-up-off" title="This answer is useful">up vote</a>2<a class="vote-down-off" title="This answer is not useful">down vote</a>

 | 

You can try [gitu](https://www.npmjs.com/package/git-upload).

For the first time (node js has to be installed):

<code>npm install -g git-upload</code> 

After that:

<code>gitu COMMIT_MSG</code> 

To issue those three commands at once.

The good thing is that you **don't have to worry when you reinstall your system or when you want to do this on different computers and No file modification is needed.** This also **work on different platforms** (not just Linux and Mac, but also Windows) just that you have to install `npm` and `nodejs` (`git` of course).

| 
 [share](https://stackoverflow.com/a/41366192 "short permalink to this answer")[improve this answer](https://stackoverflow.com/posts/41366192/edit)

 | 

 [edited May 13 at 10:07](https://stackoverflow.com/posts/41366192/revisions "show all edits to this post")

 | 

 answered Dec 28 '16 at 16:39

 ![](https://graph.facebook.com/100001696341496/picture?type=large)

 [Hellow Hi](https://stackoverflow.com/users/3913932/hellow-hi)
 4918

 |

 |
|   | 
 <a class="js-add-link comments-link disabled-link " title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”.">add a comment</a>

 |

<a name="34118289"></a>

| 
 <a class="vote-up-off" title="This answer is useful">up vote</a>1<a class="vote-down-off" title="This answer is not useful">down vote</a>

 | 

There are some issues with the scripts above:

shift "removes" the parameter $1, otherwise, "push" will read it and "misunderstand it".

My tip :

> git config --global alias.acpp '!git add -A && branchatu="$(git symbolic-ref HEAD 2>/dev/null)" && branchatu=${branchatu##refs/heads/} && git commit -m "$1" && shift && git pull -u origin $branchatu && git push -u origin $branchatu'

| 
 [share](https://stackoverflow.com/a/34118289 "short permalink to this answer")[improve this answer](https://stackoverflow.com/posts/34118289/edit)

 | 

 [edited Dec 6 '15 at 14:41](https://stackoverflow.com/posts/34118289/revisions "show all edits to this post")

 ![](https://i.stack.imgur.com/JrrcX.jpg?s=32&g=1)

 [Pierre.Vriens](https://stackoverflow.com/users/4640431/pierre-vriens)
 1,73851434

 | 

 answered Dec 6 '15 at 14:07

 ![](https://www.gravatar.com/avatar/33d7d37c80d8f3d1da8eecff9af0a37c?s=32&d=identicon&r=PG)

 [Rubens](https://stackoverflow.com/users/5646613/rubens)
 112

 |

 |
|   | 
 <a class="js-add-link comments-link disabled-link " title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”.">add a comment</a>

 |

<a name="38973769"></a>

| 
 <a class="vote-up-off" title="This answer is useful">up vote</a>1<a class="vote-down-off" title="This answer is not useful">down vote</a>

 | 

When you want svn-like behavior of git commit, use this in your git aliases in your .gitconfig

`commit = "!f() { git commit \"$@\" && git push; };f"`

| 
 [share](https://stackoverflow.com/a/38973769 "short permalink to this answer")[improve this answer](https://stackoverflow.com/posts/38973769/edit)

 | 

 answered Aug 16 '16 at 11:30

 ![](https://i.stack.imgur.com/8eQ6B.png?s=32&g=1)

 [Rik van der Heijden](https://stackoverflow.com/users/6721607/rik-van-der-heijden)
 112

 |

 |
|   | 
 <a class="js-add-link comments-link disabled-link " title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”.">add a comment</a>

 |

<a name="31005428"></a>

| 
 <a class="vote-up-off" title="This answer is useful">up vote</a>1<a class="vote-down-off" title="This answer is not useful">down vote</a>

 | 

As mentioned in [this](https://stackoverflow.com/a/4299159/2134166) answer, you can create a **git alias** and assign a set of commands for it. In this case, it would be:

<code>git config --global alias.add-com-push '!git add . && git commit -a -m "commit" && git push'</code> 

and use it with

<code>git add-com-push</code> 

| 
 [share](https://stackoverflow.com/a/31005428 "short permalink to this answer")[improve this answer](https://stackoverflow.com/posts/31005428/edit)

 | 

 [edited Jun 7 at 8:45](https://stackoverflow.com/posts/31005428/revisions "show all edits to this post")

 ![](https://i.stack.imgur.com/x93aw.jpg?s=32&g=1)

 [wonea](https://stackoverflow.com/users/271200/wonea)
 1,9431254110

 | 

 answered Jun 23 '15 at 14:20

 ![](https://i.stack.imgur.com/bkm3q.png?s=32&g=1)

 [cristianzamar](https://stackoverflow.com/users/2134166/cristianzamar)
 213

 |

 |
|   | 

| 

| 1 |   |

 | 
 This doesn't add anything to any of the previous answers. – [BanksySan](https://stackoverflow.com/users/442351/banksysan "8,341 reputation") [Oct 15 '15 at 22:30](https://stackoverflow.com/questions/19595067/git-add-commit-and-push-commands-in-one#comment54128119_31005428)

 |
| 

|    |   |

 | 
 I'm sorry, you are right. I think I didn't notice that Tilman Vogel's answer was the same as mine.. Should I delete it?? – [cristianzamar](https://stackoverflow.com/users/2134166/cristianzamar "21 reputation") [Oct 17 '15 at 14:33](https://stackoverflow.com/questions/19595067/git-add-commit-and-push-commands-in-one#comment54181362_31005428)

 |

 <a class="js-add-link comments-link disabled-link " title="Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”.">add a comment</a>

 |

<a name="43140789"></a>

| 
 <a class="vote-up-off" title="This answer is useful">up vote</a>0<a class="vote-down-off" title="This answer is not useful">down vote</a>

 | 

I did this .sh script for command

<code>#!/bin/sh
cd LOCALDIRECTORYNAME/  
git config --global user.email "YOURMAILADDRESS"
git config --global user.name "YOURUSERNAME"
git init
git status
git add -A && git commit -m "MASSAGEFORCOMMITS"
git push origin master</code> 

| 
 [share](https://stackoverflow.com/a/43140789 "short permalink to this answer")[improve this answer](https://stackoverflow.com/posts/43140789/edit)

 |

 |