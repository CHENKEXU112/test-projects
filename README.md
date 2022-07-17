#### Git 的三个区域

1. 工作区
  
  处理工作的区域
  
2. 暂存区
  
  临时存储，等待提交
  
3. Git 仓库
  
  最终存放区域
  

#### 三种状态

1. 已修改modified
  
  文件已修改，但还未提交到暂存区
  
2. 已暂存staged
  
  使已修改文件包含在下次的提交目录中
  
3. 已提交commited
  
  已保存在仓库中
  

#### Git 基本操作

1. 显示文件状态`git status -s`
  
2. git跟踪文件`git add XXX.txt`
  
3. 提交更新`git commit -m "添加了XXX.txt"`
  
4. 修改已提交文件后使文件变为已修改状态
  
5. 暂存已修改文件`git add XXX.txt`
  
6. 再次提交`git commit -m "修改了XXX.txt"`
  
7. 撤销文件修改`git checkout -- XXX.txt`：使工作区中对应文件**还原**为git仓库中的版本
  
8. 一次性添加多个文件到暂存区`git add .`
  
9. 取消暂存`git reset Head 文件名称`
  
10. 不暂存，直接提交到仓库：
  
  `git commit -a -m "描述消息"`
  
11. 移除文件
  
  - 从仓库和工作区**同时**移除：`git rm -f 文件名`
    
  - 只从仓库移除：`git rm --cached 文件名`
    
12. git 忽略文件
  
  `.gitignore`配置文件
  
  - 规则：
    
    ![](file://C:\Users\chenkexu\AppData\Roaming\marktext\images\2022-07-16-20-39-48-image.png?msec=1658063530608)
    
  - glob模式：
    
    1. 星号*：匹配任意长度字符
      
    2. 方括号[abc]: 匹配方括号中任意字符
      
    3. 问号？：匹配一个字符
      
    4. 方括号中使用短划线 [a-c]: 表示匹配在一个范围内的字符
      
    5. 两个星号**：表示匹配任意中间目录（a/**/b可以匹配a/b, a/c/d/f/b等）
      
  - 例子：
    
    ![](file://C:\Users\chenkexu\AppData\Roaming\marktext\images\2022-07-16-20-46-17-image.png?msec=1658063530635)
    
13. 查看提交历史`git log`
  
  查看最近两次历史`git log -2`
  
  自定义格式：
  
  ![](file://C:\Users\chenkexu\AppData\Roaming\marktext\images\2022-07-16-20-51-39-image.png?msec=1658063530619)
  
14. 回退到指定版本`git rset`
  
  - 从提交历史中获得commitID
    
  - `git reset --hard 对应版本的commitID`
    
  - 再使用`git reflog --pretty=oneline`显示全部历史
    
15. 本地仓库推送到github
  
  - https上传(首次)需要账号密码
    
    ```bash
    git remote add origin https地址
    git push -u origin master
    ```
    
    后续直接`git push`
    
  - SSH上传
    
    1. 生成SSH key
      
      在git 终端中输入
      
      ```bash
      ssh-keygen -t rsa -b 4096 -C"github注册邮箱"
      ```
      
      最后会在user/.ssh目录中生成id-rsa 和 id-rsa.pub两个文件
      
    2. 配置SSH key
      
      在github中配置ssh key，粘贴
      
    3. 推送仓库
      
      ```bash
      git remote add origin ssh地址
      git push -u origin master
      ```
      
16. 远程仓库克隆到本地
  
  ```bash
  git clone 远程地址
  ```
  

#### Git 分支

1. **master主分支**：用于保存和记录项目中已完成的功能代码
  
2. **功能分支**：临时开辟的用来开发新功能的分支，最后会合并
  
3. 查看分支列表：`git branch`星号前为当前分支
  
4. 创建新分支：`git branch 分支名字`基于当前所在的分支创建
  
5. 切换分支：`git checkout 分支名字`
  
6. 创建并切换分支`git checkout -b 分支名称`
  
7. 合并分支：在master上运行`git merge login`将login合并到master上
  
8. 删除分支：合并分支之后，将已合并的分支删除（不能处于该分支）
  
  ```bash
  git branch -d 分支名称
  ```
  
9. 解决合并冲突
  
  合并时，多个分支对同一个文件有修改，自动合并失败
  
  在vscode里解决冲突，然后再次添加到缓存区，再次提交
  
10. 上传分支（远程仓库默认为origin，第一次需使用-u）
  
  ```bash
  git push -u 远程仓库别名 本地分支名称：远程保存的分支名称
  ```
  
11. 查看远程仓库分支列表
  
  ```bash
  git remote show 远程仓库名称
  ```
  
12. 跟踪分支（从远程仓库下载分支）
  
  直接使用`git checkout 远程分支名称`
  
  - 需要重命名时：
    
    ```bash
    git checkout -b 本地名称 仓库名称/远程分支名称
    ```
    
13. 同步远程代码`git pull`
