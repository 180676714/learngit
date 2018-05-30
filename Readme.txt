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