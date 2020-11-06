>> 场景说明

>>> 运行git branch -a 之后发现与仓库的分支信息不一样
    ```
    > git branch -a
     *dev
      remotes/origin/dev
      remotes/origin/fixbug  // 仓库里已删除这个分支了不应该存在
    ```
>> 解决方法

  使用git remote prune origin 清理origin远程仓库映射

>> 其它相关

  使用git remote update 更新映射
  
