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
						