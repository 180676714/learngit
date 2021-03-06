Git Learn:

Learn one:
//创建版本库
	git init 				//构建一个git仓库
	
	//添加文件到git仓库，一共分两步
	git add Readme.txt			//第一步：添加Readme.txt文件到git仓库
	git commit -m "添加Readme.txt文件"	//第二部：使用git commit命令，完成

Learn two:
//时光机穿梭
	git status				//git status命令，时刻掌握git仓库当前的状态
	git diff "Readme.txt"			//查看文件具体修改了哪些内容
	git diff HEAD -- Readme.txt		//查看工作区和版本库里面最新版本的区别

	//提交修改和提交更新一样分两步
	git add Readme.txt			//第一步：添加Readme.txt文件到git仓库
	git commit -m "添加Readme.txt文件"	//第二部：使用git commit命令，完成

Learn three:
//版本回退
	git log					//查看从近到远的提交日志
	git log --pretty=oneline		//去掉乱七八糟的历史信息，只保留提交版本号

	//HEAD表示当前的版本
	//HEAD^表示上一个版本 HEAD^^表示上上一个版本 HEAD～100表示上100个版本
	git reset --hard HEAD^			//使用git reset命令回退到以前的版本
	git reset --hard bcc233			//回到某一个版本，包括未来的版本，我胡汉三又回来了
	
	cat Readme.txt				//查看内容
	
	git reflog				//记录你的每一次命令

Learn four:
//撤销修改
	//就是让文件回到最近一次git commit或git add时的状态
	//git checkout -- file 中的‘--’很重要，如果没有‘--’此命令就变成了“创建一个新分支”

	git checkout -- Readme.txt		//把Readme.txt文件在工作区的修改全部撤销掉

	//小结
	//场景一：当你搞乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令git checkout -- file
	//场景二：当你搞乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改,分两步，第一步用命令git reset HEAD file,就回到场景一了，第二步，按场景一操作
	//场景三：已经提交了不合适的剧改到版本库时，想要撤销本次提交，参考回退命令，不过前提是没有推送到远程库。

Learn five:
//删除操作
	rm test.txt				//删除test.txt文件
	git commit -m 'xxx'			//提交，修改版本库的状态

	//如果是误操作删除，使用命令rm file，只是删除了工作区，这时候版本库中还存在，那可以使用git checkout -- file命令恢复
	git checkout -- 'xxx'			//从版本库中恢复工作区中误删的文件

Learn six:
//远程仓库
	//关联远程仓库
	git remote add origin git@server-name:path/repo-name.git
	//关联后，推送master分支的所有内容到远程库
	git push -u origin master
	//从远程库客隆
	git clone git@server-name:path/repo-name.git

Learn seven:
//分支管理
	//第一步：创建dev分支，然后切换到dev分支上；
	git checkout -b dev
	//'-b'参数表示创建并切换，相当于下面两条命令
	git branch dev
	git checkout dev
	
	//第二步：用git branch命令查看当前分支
	git branch

	//第三步：切换回master branch
	git checkout master

	//第四步：把dev分支的工作成果合并到master分支
	git merge dev

	//第五步：合并完成之后，就可以放心的删除dev分支了
	git branch -d dev

Learn eight:
//解决冲突
	//查看分支合并情况
	git log --graph --pretty=oneline --abbrev-commit

Learn nine:
//分支策略
	//禁用‘fast forward’模式，git就会在merge时生成一个新的commit，这样，从分支历史上就可以查看出分支信息

	//下⾯面我们实战⼀一下--no-ff⽅方式的merge:
	//首先，仍然创建并切换dev分⽀支:
	git checkout -b dev

	//修改readme.txt⽂文件，并提交⼀一个新的commit:
	git add readme.txt
	git commit -m "add merge"				
	
	//现在，我们切换回master:
	git checkout master

	//准备合并dev分⽀支，请注意--no-ff参数，表⽰示禁⽤用“Fast forward”:
	git merge --no-ff -m "merge with no-ff" dev

	//因为本次合并要创建⼀一个新的commit，所以加上-m参数，把commit描述写进去。 合并后，我们⽤用git log看看分⽀支历史:
	git log --graph --pretty=oneline --abbrev-commit

	//可以看到，使用和不使⽤“Fast forward”模式，是有区别的，区别在于：合并分支时，加上--no-ff参数就可以用普通模式合并，合并后的历史有分⽀支，能看出来曾经 做过合并，⽽而fast forward合并就看不出来曾经做过合并。

Learn ten:
//bug分支
	//Git还提供了⼀一个stash功能，可以把当前⼯工作现场“储藏”起来，等以后恢复现场后 继续⼯工作:
	git stash
	
	//工作区是干净的，刚才的⼯工作现场存到哪去了?⽤用git stash list命令看看:
	git stash list

	//工作现场还在，Git把stash内容存在某个地⽅方了，但是需要恢复⼀一下，有两个办法:
	//一是⽤用git stash apply恢复，但是恢复后，stash内容并不删除，你需要⽤用git stash drop来删 除;
	//另⼀一种⽅方式是⽤用git stash pop，恢复的同时把stash内容也删了:
	git stash pop

	//再⽤用git stash list查看，就看不到任何stash内容了:
	git stash list

	//你可以多次stash，恢复的时候，先⽤用git stash list查看，
	//然后恢复指定的stash，⽤用命令: 
	git stash apply stash@{0}

	//小结
	//修复bug时，我们会通过创建新的bug分⽀支进⾏行修复，然后合并，最后删除;
	//当手头⼯工作没有完成时，先把⼯工作现场git stash⼀一下，然后去修复bug，
	//修复后，再git stash pop，回到⼯工作现场。

Learn eleven:
//多人协作
	//多⼈协作的⼯工作模式通常是这样:
	1. ⾸首先，可以试图⽤用git push origin branch-name推送⾃自⼰己的修改;
	2. 如果推送失败，则因为远程分⽀支⽐比你的本地更新，需要先⽤用git pull试图合并;
	3. 如果合并有冲突，则解决冲突，并在本地提交;
	4. 没有冲突或者解决掉冲突后，再⽤用git push origin branch-name推送就能成功!   
	如果git pull提⽰示“no tracking information”，则说明本地分⽀支和远程分⽀支的链接关系没
	有创建，⽤用命令git branch --set-upstream branch-name origin/branch-name。 这就是多⼈	人协作的⼯工作模式，⼀一旦熟悉了，就⾮非常简单。

	小结
	• 查看远程库信息，使⽤用git remote -v;
	• 本地新建的分⽀支如果不推送到远程，对其他⼈人就是不可⻅见的;
	• 从本地推送分⽀支，使⽤用git push origin branch-name，如果推送失败，先⽤用git pull抓 取远	程的新提交;
	• 在本地创建和远程分⽀支对应的分⽀支，使⽤用git checkout -b branch-name origin/branch- 	name，本地和远程分⽀支的名称最好⼀一致;
	• 建⽴立本地分⽀支和远程分⽀支的关联，使⽤用git branch --set-upstream branch-name origin/	branch-name;
	• 从远程抓取分⽀支，使⽤用git pull，如果有冲突，要先处理冲突。

Learn twelve:
//标签管理
	
	• 命令git tag name⽤用于新建⼀一个标签，默认为HEAD，也可以指定⼀一个commit id;
	• -a tagname -m "blablabla..."可以指定标签信息;
	• -s tagname -m "blablabla..."可以⽤用PGP签名标签;
	• 命令git tag可以查看所有标签;

//标签操作
	• 命令git push origin tagname可以推送⼀一个本地标签;
	• 命令git push origin --tags可以推送全部未推送过的本地标签;
	• 命令git tag -d tagname可以删除⼀一个本地标签;
	• 命令git push origin :refs/tags/tagname可以删除⼀一个远程标签。
	
						