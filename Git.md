新建Dev分支并且切换到此Dev分支上    git checkout -b dev（分支名：名字+做的事）   
                                                            git checkout dev（有次分支就会切换回次分支）
新建合并请求：pull request 
        1.选择 xx基于 和 xx对比 合并请求；
        2. 合并请求作出的修改；
                3. 编辑    评审者； 
                4.确定；
                5. 评审者确定是否xx文件的合并；
            选项：删除原分支  模式

解决冲突 ： git rebase
	1. 
切换回dev分支                                          git checkout dev 
	2. 
拉取现在最新的dev的代码                         git pull origin dev
	3. 
返回到合并的分支上                                   git checkout new
	4. 
两者之间进行比较  变基                              git rebase dev
	5. 
解决完冲突后要把代码添加到缓存区            git add .
	6. 
继续                                                           git rebase --continue


            比较完成后要添加缓存区，countinue直到出现applying为止，冲突才解决完成
     7. 解决后的项目        git push origin dev
    
    * 
有冲突就pull下来再次比较，直到出现applying为止，

