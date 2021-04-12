# 1. 对比文件
![](https://camo.githubusercontent.com/cadc4780c37a1d56dbd0c96ef4634d5e3ef6fce59d09861cab593096d638bc9c/68747470733a2f2f696d672d626c6f672e6373646e696d672e636e2f323032303035313531393038303931312e706e67)

通过git log 查看以前的信息。

```shell
git diff HEAD HEAD^ -- 文件名
```
HEAD表示当前的版本，HEAD^ 表示上一个版本。

# 2. 文件删除
- 删除没有添加进版本库中的工作区中的文件，那直接删除不用做任何操作。

- 如果已添加进工作区但没有提交的文件，先要先撤回工作区
  - 比如，现在我写了一个文件添加到版本库.txt。
  ![](https://camo.githubusercontent.com/0ca1772b8064d848f5cb4228971bd8dbab1d6e3f59ff3ad6554c7999a52c1f4b/68747470733a2f2f696d672d626c6f672e6373646e696d672e636e2f32303230303531353139313234353233332e706e67)
  先提交下，git status 查看状态，绿色就是在版本库。
  ![](https://camo.githubusercontent.com/0b32cb3c052853f19ec8caba466f96a994932636b8cb03e2bb16bec30d8f2266/68747470733a2f2f696d672d626c6f672e6373646e696d672e636e2f323032303035313531393134333032362e706e67)
    ```
     git reset HEAD
    ```
    就可以撤销了，不行git status 查看状态，红色就是在工作区。
    ![](https://camo.githubusercontent.com/9415c02215c66012060308102bb83aa90d8b1141a63d14607b312b1953e2435e/68747470733a2f2f696d672d626c6f672e6373646e696d672e636e2f32303230303531353139313734383530342e706e67)
    如果我已提交到版本库，突然间我发现写错了代码，老板看了，肯定扣我工资 ，不行，我赶紧要回来。
    ![](https://camo.githubusercontent.com/0097739c35a5aa4ea078454c918102e6f7c4eaae1f9171e1d68bda2ca48e2ba5/68747470733a2f2f696d672d626c6f672e6373646e696d672e636e2f32303230303531353139323533323337362e706e673f)

    去码云看看，发现存在了。现在怎么把这个文件撤回呢？
    ![](https://camo.githubusercontent.com/6f0c12cbb5401365b7243a61bdba4a48789566913824d461513386b2fba554c3/68747470733a2f2f696d672d626c6f672e6373646e696d672e636e2f32303230303531353139323631353834312e706e67)

    有人说，我直接去Github码云上删除，恩，是一种办法，而且是一个猪办法!

    如果项目不是在你的账号创建的，就没资格用客户端删东西。

    答案就是回滚，再提交，只需要执行：
    ```
    git revert HEAD
    git push
    ```
    ![](https://camo.githubusercontent.com/475f25a7852d6587d1d8cbe130b1c56457ccdc5098743a6fb5d62274445904fa/68747470733a2f2f696d672d626c6f672e6373646e696d672e636e2f32303230303531353139333734383635362e706e67)

    这时候就没有了.
    ![](https://camo.githubusercontent.com/bb1943cc04c47b970ebe8f5cbacabe8f377a78e095b2c25d99d5fb57b739983a/68747470733a2f2f696d672d626c6f672e6373646e696d672e636e2f32303230303531353139333830393838372e706e67)

# 3. 创建分支

正常的开发项目中都是多人协作，每个人的任务一般不会一天就完成，如果把没有完成的代码提交到远程仓库会影响被人工作。git提供了分支的功能就不用担心了，可以创建一个自己的分支，在上面干活，想提交就提交，等到工作完成再一次性合并到原来的分支。

新建git仓库时会默认创建一个分支master，它叫主分支。一般情况我们不会直接在主分支上干活，它主要用来发布版本。

我创建一个开发分支develop
```
git branch develop
```

再切换到develop分支
```
git checkout develop
```
![](https://camo.githubusercontent.com/da8c7c936509c813fab39ae1a7c8bd443483a53c28f6125f7d5084b63d3bcf7f/68747470733a2f2f696d672d626c6f672e6373646e696d672e636e2f32303230303531353139343134383133302e706e67)
使用git branch命令查看当前分支。-b参数表示创建并切换。

如果想创建的时候，直接切换，直接-b参数
```
git checkout-b  develop 
```

# 4. 合并分支
创建好develop分支，菜比的我，24小时之后开发完毕，提交：
![](https://camo.githubusercontent.com/1833e1ec2818c7ee6d78699e4220003d918f04006034f1329a518ecec5007d50/68747470733a2f2f696d672d626c6f672e6373646e696d672e636e2f32303230303531353139343532353137312e706e67)
```
$ git add .
$ git commit -m '24小时之后开发完毕'
```
![](https://camo.githubusercontent.com/229cd97743e89bd1ec42e0f6210a44d3675338ee412f3694b89a81c984fb7cc1/68747470733a2f2f696d672d626c6f672e6373646e696d672e636e2f32303230303531353139343632353631372e706e67)

现在切换到master
```
$ git checkout master
Switched to branch 'master'
```
查看工作区，你会发现刚才写的文件没有了，不要惊慌，因为那个提交是在develop分支上，现在Runsne把develop分支的工作合并到master分支上：
![](https://camo.githubusercontent.com/fa42f6a57fbff190e9a90c076d4c16591feffe809aa7683331bbbc081f760859/68747470733a2f2f696d672d626c6f672e6373646e696d672e636e2f32303230303531353139343830333531392e706e67)

```
git merge develop
```
![](https://camo.githubusercontent.com/9d05916c1ba6e1103d0de7e1e8b113978fd3c3c6ee3f63ea26f25ffee906de0c/68747470733a2f2f696d672d626c6f672e6373646e696d672e636e2f32303230303531353139343835373232362e706e67)

这个时候就出现了

![](https://camo.githubusercontent.com/61148ee5c8faab0b86ba212d3dfbda053dd0b1cbebe98ab6cb4c0ed5b9e0122f/68747470733a2f2f696d672d626c6f672e6373646e696d672e636e2f32303230303531353139343931373834342e706e67)

# 5. 删除分支
合并完之后你也可以删除掉develop分支：
```
$ git branch -d develop
Deleted branch develop (was 25942c9)).
$ git branch
* master
```
![](https://camo.githubusercontent.com/0c90053efe9f056dc191d2ff818c143cf80db698caad85dba4871606c2c63453/68747470733a2f2f696d672d626c6f672e6373646e696d672e636e2f32303230303531353139353130393630382e706e67)

OK搞定，把之前的Git文章全部删除

![](https://camo.githubusercontent.com/6abb949b57da2c7bbc062c5e36fd7669abe77f9b6de334a459240bcb4bab809f/68747470733a2f2f696d672d626c6f672e6373646e696d672e636e2f32303230303531353139353233343131372e706e67)