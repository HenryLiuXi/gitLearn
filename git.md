<!-- 创建版本库 -->
<!-- 操作命令 -->
<!-- 添加某个文件时，该文件必须在当前目录下存在，用ls或者dir命令查看当前目录的文件，看看文件是否存在，或者是否写错了文件名。 -->
<!-- 什么是版本库呢？版本库又名仓库，英文名repository，你可以简单理解成一个目录，这个目录里面的所有文件都可以被Git管理起来，每个文件的修改、删除，Git都能跟踪，以便任何时刻都可以追踪历史，或者在将来某个时刻可以“还原”。
所以，创建一个版本库非常简单，首先，选择一个合适的地方，创建一个空目录： 
第一步
-->
mkdir <文件夹名>
cd <文件夹名>
<!-- pwd命令用于显示当前目录。在我的Mac上，这个仓库位于/Users/michael/learngit。 -->
pwd           

<!-- 第二步  通过git init命令把这个目录变成Git可以管理的仓库：-->
git init
<!-- 瞬间Git就把仓库建好了，而且告诉你是一个空的仓库（empty Git repository），细心的读者可以发现当前目录下多了一个.git的目录，这个目录是Git来跟踪管理版本库的，没事千万不要手动修改这个目录里面的文件，不然改乱了，就把Git仓库给破坏了。
如果你没有看到.git目录，那是因为这个目录默认是隐藏的，用ls -ah命令就可以看见。 
也不一定必须在空目录下创建Git仓库，选择一个已经有东西的目录也是可以的。-->
<!-- =========================================================================================================== -->
<!-- 一定要放到learngit目录下（子目录也行），因为这是一个Git仓库，放到其他地方Git再厉害也找不到这个文件。
和把大象放到冰箱需要3步相比，把一个文件放到Git仓库只需要两步。 -->
<!-- 第一步，用命令git add告诉Git，把文件添加到仓库： -->
git add <指定文件名>
<!-- 也可以通过 'git add .'将当前文件夹所以文件提交 -->
<!-- 执行上面的命令，没有任何显示，这就对了，Unix的哲学是“没有消息就是好消息”，说明添加成功。 -->

<!-- 第二步，用命令git commit告诉Git，把文件提交到仓库： -->
git commit -m '本次提交的说明'

<!-- 时光机穿梭 版本切换 -->
<!-- git status命令可以让我们时刻掌握仓库当前的状态  要随时掌握工作区的状态，使用git status命令-->
git status

<!-- git diff顾名思义就是查看difference，显示的格式正是Unix通用的diff格式，可以显示文件名目前产品与上个版本存成的差异。如果‘git status’告诉你有文件被修改过，用‘git diff’可以查看修改内容 -->
git diff <文件名>

<!-- 用HEAD表示当前版本 上一个版本就是HEAD^ 上上一个版本就是HEAD^^ 当然往上100个版本写100个^比较容易数不过来，所以写成HEAD~100-->
git reset --hard HEAD^

<!-- HEAD指向的版本就是当前版本，因此，Git允许我们在版本的历史之间穿梭，使用命令git reset --hard commit_id -->
git reset --hard <版本ID>

<!-- 穿梭前，用git log可以查看提交历史，以便确定要回退到哪个版本 -->
git log

<!-- 要重返未来，用git reflog查看命令历史，以便确定要回到未来的哪个版本。 -->
git reflog

<!-- ======================================================================================================================= -->
<!-- 工作区有一个隐藏目录.git，这个不算工作区，而是Git的版本库。 -->
<!-- 工作区有一个隐藏目录.git，这个不算工作区，而是Git的版本库。
Git的版本库里存了很多东西，其中最重要的就是称为stage（或者叫index）的暂存区，还有Git为我们自动创建的第一个分支master，以及指向master的一个指针叫HEAD。 
可以参考图片

前面讲了我们把文件往Git版本库里添加的时候，是分两步执行的：

第一步是用git add把文件添加进去，实际上就是把文件修改添加到暂存区；
第二步是用git commit提交更改，实际上就是把暂存区的所有内容提交到当前分支。
-->
<!-- 如果不用git add到暂存区，那就不会加入到commit中 -->

<!-- git checkout -- file可以丢弃工作区的修改： -->
git checkout -- <文件名>
<!-- git checkout -- file命令中的--很重要，没有--，就变成了“切换到另一个分支”的命令，我们在后面的分支管理中会再次遇到git checkout命令。 -->

<!-- 用命令git reset HEAD <file>可以把暂存区的修改撤销掉（unstage），重新放回工作区： -->
git reset HEAD <文件名>
<!-- git reset命令既可以回退版本，也可以把暂存区的修改回退到工作区。当我们用HEAD时，表示最新的版本。 -->

<!-- 删除文件 -->
<!-- 一般情况下，你通常直接在文件管理器中把没用的文件删了，或者用rm命令删了： -->
rm <文件名>
<!-- Git知道你删除了文件，因此，工作区和版本库就不一致了，git status命令会立刻告诉你哪些文件被删除了： -->
<!-- 现在你有两个选择，一是确实要从版本库中删除该文件，那就用命令git rm删掉，并且git commit： -->
<!-- 命令git rm用于删除一个文件。如果一个文件已经被提交到版本库，那么你永远不用担心误删，但是要小心，你只能恢复文件到最新版本，你会丢失最近一次提交后你修改的内容 -->
git rm <文件名>


<!-- 目前，在GitHub上的这个learngit仓库还是空的，GitHub告诉我们，可以从这个仓库克隆出新的仓库，也可以把一个已有的本地仓库与之关联，然后，把本地仓库的内容推送到GitHub仓库。
现在，我们根据GitHub的提示，在本地的learngit仓库下运行命令： -->

git remote add origin 'git地址'




<!-- ============================================================================================================================================ -->
<!-- 远程仓库 -->
<!-- 第1步：创建SSH Key。在用户主目录下，看看有没有.ssh目录，如果有，再看看这个目录下有没有id_rsa和id_rsa.pub这两个文件，如果已经有了，可直接跳到下一步。如果没有，打开Shell（Windows下打开Git Bash），创建SSH Key： -->
ssh-keygen -t rsa -C "邮箱名"
<!-- 你需要把邮件地址换成你自己的邮件地址，然后一路回车，使用默认值即可，由于这个Key也不是用于军事目的，所以也无需设置密码。
如果一切顺利的话，可以在用户主目录里找到.ssh目录，里面有id_rsa和id_rsa.pub两个文件，这两个就是SSH Key的秘钥对，id_rsa是私钥，不能泄露出去，id_rsa.pub是公钥，可以放心地告诉任何人。
第2步：登陆GitHub，打开“Account settings”，“SSH Keys”页面：
然后，点“Add SSH Key”，填上任意Title，在Key文本框里粘贴id_rsa.pub文件的内容 -->

<!-- 我们根据GitHub的提示，在本地的learngit仓库下运行命令： -->
git remote add origin <SSH链接>
<!-- 远程库的名字就是origin，这是Git默认的叫法，也可以改成别的，但是origin这个名字一看就知道是远程库。 -->

<!-- git push命令，实际上是把当前分支master推送到远程。 -->
git push -u origin master
<!-- 由于远程库是空的，我们第一次推送master分支时，加上了-u参数，Git不但会把本地的master分支内容推送的远程新的master分支，还会把本地的master分支和远程的master分支关联起来，在以后的推送或者拉取时就可以简化命令。 -->

<!-- 从现在起，只要本地作了提交，就可以通过命令： -->
git push origin master

<!-- 要关联一个远程库，使用命令git remote add origin  <SSH链接>；
关联后，使用命令git push -u origin master第一次推送master分支的所有内容；
此后，每次本地提交后，只要有必要，就可以使用命令git push origin master推送最新修改；
 -->


<!-- ============================================================================================================= -->
<!-- 分支管理 -->
<!-- 一开始的时候，master分支是一条线，Git用master指向最新的提交，再用HEAD指向master，就能确定当前分支，以及当前分支的提交点：图一 
每次提交，master分支都会向前移动一步，这样，随着你不断提交，master分支的线也越来越长。-->
<!-- 当我们创建新的分支，例如dev时，Git新建了一个指针叫dev，指向master相同的提交，再把HEAD指向dev，就表示当前分支在dev上：图二 
你看，Git创建一个分支很快，因为除了增加一个dev指针，改改HEAD的指向，工作区的文件都没有任何变化！-->
<!-- 从现在开始，对工作区的修改和提交就是针对dev分支了，比如新提交一次后，dev指针往前移动一步，而master指针不变：图三 -->
<!-- 假如我们在dev上的工作完成了，就可以把dev合并到master上。Git怎么合并呢？最简单的方法，就是直接把master指向dev的当前提交，就完成了合并：图四 -->
<!-- 所以Git合并分支也很快！就改改指针，工作区内容也不变！
合并完分支后，甚至可以删除dev分支。删除dev分支就是把dev指针给删掉，删掉后，我们就剩下了一条master分支：图五 -->

<!-- 首先，我们创建dev分支，然后切换到dev分支： -->
git checkout -b dev
<!-- git checkout命令加上-b参数表示创建并切换，相当于以下两条命令： -->
git branch dev
git checkout dev

<!-- 用git branch命令查看当前分支： 
git branch命令会列出所有分支，当前分支前面会标一个*号。-->
git branch

<!-- 我们把dev分支的工作成果合并到master分支上： -->
git merge dev

<!-- 合并完成后，就可以放心地删除dev分支了： -->
git branch -d dev

<!-- 删除后，查看branch，就只剩下master分支了： -->
git branch

<!-- 因为创建、合并和删除分支非常快，所以Git鼓励你使用分支完成某个任务，合并后再删掉分支，这和直接在master分支上工作效果是一样的，但过程更安全。 -->

<!-- switch
我们注意到切换分支使用git checkout <branch>，而前面讲过的撤销修改则是git checkout -- <file>，同一个命令，有两种作用，确实有点令人迷惑。
实际上，切换分支这个动作，用switch更科学。因此，最新版本的Git提供了新的git switch命令来切换分支：
创建并切换到新的dev分支，可以使用： -->
git switch -c dev

<!-- 直接切换到已有的master分支，可以使用： -->
git switch master

<!-- Git鼓励大量使用分支
查看分支：git branch
创建分支：git branch <name>
切换分支：git checkout <name>或者git switch <name>
创建+切换分支：git checkout -b <name>或者git switch -c <name>
合并某分支到当前分支：git merge <name>
删除分支：git branch -d <name> -->

<!-- 解决分支冲突 -->

<!-- 当Git无法自动合并分支时，就必须首先解决冲突。解决冲突后，再提交，合并完成。
解决冲突就是把Git合并失败的文件手动编辑为我们希望的内容，再提交。
用git log --graph命令可以看到分支合并图。 -->

<!-- 通常，合并分支时，如果可能，Git会用Fast forward模式，但这种模式下，删除分支后，会丢掉分支信息。
如果要强制禁用Fast forward模式，Git就会在merge时生成一个新的commit，这样，从分支历史上就可以看出分支信息。
下面我们实战一下--no-ff方式的git merge： -->

<!-- 分支策略
在实际开发中，我们应该按照几个基本原则进行分支管理：
首先，master分支应该是非常稳定的，也就是仅用来发布新版本，平时不能在上面干活；
那在哪干活呢？干活都在dev分支上，也就是说，dev分支是不稳定的，到某个时候，比如1.0版本发布时，再把dev分支合并到master上，在master分支发布1.0版本；
你和你的小伙伴们每个人都在dev分支上干活，每个人都有自己的分支，时不时地往dev分支上合并就可以了。
所以，团队合作的分支看起来就像这样： -->
<!-- Git分支十分强大，在团队开发中应该充分应用。
合并分支时，加上--no-ff参数就可以用普通模式合并，合并后的历史有分支，能看出来曾经做过合并，而fast forward合并就看不出来曾经做过合并。 -->

<!-- Bug分支

并不是你不想提交，而是工作只进行到一半，还没法提交，预计完成还需1天时间。但是，必须在两个小时内修复该bug，怎么办？
幸好，Git还提供了一个stash功能，可以把当前工作现场“储藏”起来，等以后恢复现场后继续工作： -->
git stash
<!-- 现在，用git status查看工作区，就是干净的（除非有没有被Git管理的文件），因此可以放心地创建分支来修复bug。 -->

<!-- 工作区是干净的，刚才的工作现场存到哪去了？用git stash list命令看看： -->
git stash list

<!-- 工作现场还在，Git把stash内容存在某个地方了，但是需要恢复一下，有两个办法：
一是用git stash apply恢复，但是恢复后，stash内容并不删除，你需要用git stash drop来删除；
另一种方式是用git stash pop，恢复的同时把stash内容也删了： -->
<!-- 再用git stash list查看，就看不到任何stash内容了： -->
<!-- 你可以多次stash，恢复的时候，先用git stash list查看，然后恢复指定的stash，用命令： 
stash@{0}为stash的哪一个
-->
git stash apply stash@{0}

<!-- 在master分支上修复了bug后，我们要想一想，dev分支是早期从master分支分出来的，所以，这个bug其实在当前dev分支上也存在。
那怎么在dev分支上修复同样的bug？重复操作一次，提交不就行了？
有木有更简单的方法？
有！
同样的bug，要在dev上修复，我们只需要把4c805e2 fix bug 101这个提交所做的修改“复制”到dev分支。注意：我们只想复制4c805e2 fix bug 101这个提交所做的修改，并不是把整个master分支merge过来。
为了方便操作，Git专门提供了一个cherry-pick命令，让我们能复制一个特定的提交到当前分支： -->

<!-- 修复bug时，我们会通过创建新的bug分支进行修复，然后合并，最后删除；
当手头工作没有完成时，先把工作现场git stash一下，然后去修复bug，修复后，再git stash pop，回到工作现场；
在master分支上修复的bug，想要合并到当前dev分支，可以用git cherry-pick <commit>命令，把bug提交的修改“复制”到当前分支，避免重复劳动。 -->

<!-- Feature分支 -->
<!-- 开发一个新feature，最好新建一个分支；
如果要丢弃一个没有被合并过的分支，可以通过git branch -D <name>强行删除。 -->
git branch -D <name>

<!-- 多人协作 -->
<!-- 当你从远程仓库克隆时，实际上Git自动把本地的master分支和远程的master分支对应起来了，并且，远程仓库的默认名称是origin。
要查看远程库的信息，用git remote： -->
git remote
<!-- 或者，用git remote -v显示更详细的信息： 
 git remote -v
origin  git@github.com:michaelliao/learngit.git (fetch)
origin  git@github.com:michaelliao/learngit.git (push)-->
git remote -v

<!-- 推送分支
推送分支，就是把该分支上的所有本地提交推送到远程库。推送时，要指定本地分支，这样，Git就会把该分支推送到远程库对应的远程分支上： -->
git push origin <name>
<!-- 如果要推送其他分支，比如dev，就改成： -->
git push origin dev

<!-- 那么，哪些分支需要推送，哪些不需要呢？
master分支是主分支，因此要时刻与远程同步；
dev分支是开发分支，团队所有成员都需要在上面工作，所以也需要与远程同步；
bug分支只用于在本地修复bug，就没必要推到远程了，除非老板要看看你每周到底修复了几个bug；
feature分支是否推到远程，取决于你是否和你的小伙伴合作在上面开发。
总之，就是在Git中，分支完全可以在本地自己藏着玩，是否推送，视你的心情而定！ -->

<!-- 小结
查看远程库信息，使用git remote -v；
本地新建的分支如果不推送到远程，对其他人就是不可见的；
从本地推送分支，使用git push origin branch-name，如果推送失败，先用git pull抓取远程的新提交；
在本地创建和远程分支对应的分支，使用git checkout -b branch-name origin/branch-name，本地和远程分支的名称最好一致；
建立本地分支和远程分支的关联，使用git branch --set-upstream branch-name origin/branch-name；
从远程抓取分支，使用git pull，如果有冲突，要先处理冲突。 -->

<!-- 我们输入命令git rebase试试： -->
git rebase
<!-- 输出了一大堆操作，到底是啥效果？再用git log看看： -->
<!-- 原本分叉的提交现在变成一条直线了！这种神奇的操作是怎么实现的？其实原理非常简单。我们注意观察，发现Git把我们本地的提交“挪动”了位置，放到了f005ed4 (origin/master) set exit=1之后，这样，整个提交历史就成了一条直线。rebase操作前后，最终的提交内容是一致的，但是，我们本地的commit修改内容已经变化了，它们的修改不再基于d1be385 init hello，而是基于f005ed4 (origin/master) set exit=1，但最后的提交7e61ed4内容是一致的。
这就是rebase操作的特点：把分叉的提交历史“整理”成一条直线，看上去更直观。缺点是本地的分叉提交已经被修改过了。
最后，通过push操作把本地分支推送到远程： -->
<!-- 小结
rebase操作可以把本地未push的分叉提交历史整理成直线；
rebase的目的是使得我们在查看历史提交的变化时更容易，因为分叉的提交需要三方对比。 -->

<!-- 标签管理
发布一个版本时，我们通常先在版本库中打一个标签（tag），这样，就唯一确定了打标签时刻的版本。将来无论什么时候，取某个标签的版本，就是把那个打标签的时刻的历史版本取出来。所以，标签也是版本库的一个快照。
Git的标签虽然是版本库的快照，但其实它就是指向某个commit的指针（跟分支很像对不对？但是分支可以移动，标签不能移动），所以，创建和删除标签都是瞬间完成的。
Git有commit，为什么还要引入tag？
“请把上周一的那个版本打包发布，commit号是6a5819e...”
“一串乱七八糟的数字不好找！”
如果换一个办法：
“请把上周一的那个版本打包发布，版本号是v1.2”
“好的，按照tag v1.2查找commit就行！”
所以，tag就是一个让人容易记住的有意义的名字，它跟某个commit绑在一起。 -->

<!-- 在Git中打标签非常简单，首先，切换到需要打标签的分支上： -->
git branch
git checkout master
<!-- 然后，敲命令git tag <name>就可以打一个新标签： -->
git tag v1.0

<!-- 可以用命令git tag查看所有标签： -->
git tag

<!-- 默认标签是打在最新提交的commit上的。有时候，如果忘了打标签，比如，现在已经是周五了，但应该在周一打的标签没有打，怎么办？
方法是找到历史提交的commit id，然后打上就可以了： -->
git log --pretty=oneline --abbrev-commit
<!-- 比方说要对某个这次提交打标签，它对应的commit id是f52c633，敲入命令： -->
git tag v0.9 f52c633
<!-- 再用命令git tag查看标签： -->
git tag
<!-- 注意，标签不是按时间顺序列出，而是按字母排序的。可以用git show <tagname>查看标签信息： -->
git show v0.9
<!-- 可以看到，v0.9确实打在add merge这次提交上。
还可以创建带有说明的标签，用-a指定标签名，-m指定说明文字： -->
git tag -a v0.1 -m "version 0.1 released" 1094adb
<!-- 用命令git show <tagname>可以看到说明文字： -->
git show v1.0

<!-- 小结
命令git tag <tagname>用于新建一个标签，默认为HEAD，也可以指定一个commit id；
命令git tag -a <tagname> -m "blablabla..."可以指定标签信息；
命令git tag可以查看所有标签。 -->

<!-- 操作标签
如果标签打错了，也可以删除：git tag -d v1.0-->
git tag -d v1.0
<!-- 因为创建的标签都只存储在本地，不会自动推送到远程。所以，打错的标签可以在本地安全删除。
如果要推送某个标签到远程，使用命令git push origin <tagname>： -->
git push origin v1.0

<!-- 一次性推送全部尚未推送到远程的本地标签： -->
git push origin --tags

<!-- 如果标签已经推送到远程，要删除远程标签就麻烦一点，先从本地删除： -->
git tag -d v1.0
<!-- 然后，从远程删除。删除命令也是push，但是格式如下： -->
git push origin :refs/tags/v1.0
<!-- 要看看是否真的从远程库删除了标签，可以登陆GitHub查看。 -->

<!-- 小结
命令git push origin <tagname>可以推送一个本地标签；
命令git push origin --tags可以推送全部未推送过的本地标签；
命令git tag -d <tagname>可以删除一个本地标签；
命令git push origin :refs/tags/<tagname>可以删除一个远程标签。 -->

<!-- 配置别名 -->
<!-- 有没有经常敲错命令？比如git status？status这个单词真心不好记。
如果敲git st就表示git status那就简单多了，当然这种偷懒的办法我们是极力赞成的。
我们只需要敲一行命令，告诉Git，以后st就表示status： -->

git config --global alias.st status
<!-- 好了，现在敲git st看看效果。 -->
git st

<!-- 当然还有别的命令可以简写，很多人都用co表示checkout，ci表示commit，br表示branch： -->
git config --global alias.co checkout
git config --global alias.ci commit
git config --global alias.br branch
<!-- --global参数是全局参数，也就是这些命令在这台电脑的所有Git仓库下都有用。 -->

<!-- 在撤销修改一节中，我们知道，命令git reset HEAD file可以把暂存区的修改撤销掉（unstage），重新放回工作区。既然是一个unstage操作，就可以配置一个unstage别名： -->
git config --global alias.unstage 'reset HEAD'
<!-- 当你敲入命令： -->
git unstage test.md
<!-- 实际上git执行的是 -->
git reset HEAD test.md

<!-- 配置一个git last，让其显示最后一次提交信息： -->
git config --global alias.last 'log -1'
<!-- 这样，用git last就能显示最近一次的提交： -->
git last

<!-- 甚至还有人丧心病狂地把lg配置成了： -->
git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"