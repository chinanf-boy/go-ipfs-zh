# 使用[sharness 框架](https://github.com/mlafeldt/sharness/) 进行 IPFS 的整体测试

## 运行所有测试

只需在这个目录中使用`make`，就可以运行所有的测试。带有`TEST_VERBOSE=1`可得到有帮助的详细输出.

```
TEST_VERBOSE=1 make
```

通常的 IPFS Env 参数也可以应用上:

```sh
# 这个信息的输出，可以让你的眼睛炸裂
IPFS_LOGGING=debug TEST_VERBOSE=1 make
```

要使测试在发生错误时立即中止,请使用 TEST_IMMEDIATE env 变量:

```sh
# 第一个错误产生，就中止
TEST_IMMEDIATE=1 make
```

## 只运行一个测试

你可以像一个普通的 shell 脚本一样运行一个测试脚本:

```
$ ./t0010-basic-commands.sh
```

## 调试一次测试

你可以使用`-v`选项，使它详细，和`-i`选项,就是一旦测试失败,就立即停止.例如:

```
$ ./t0010-basic-commands.sh -v -i
```

## 清晰度(Sharness)

当从主 Makefile 文件中运行清晰度测试时，或当`test_sharness_deps`目标是运行依赖项时, sharness 会从它的 github repo 下载并安装在"lib/sharness"目录中.

请不要更改"lib/sharness"目录中的任何内容.

如果你真的需要改变 sharness,请把它从[规定 库](https://github.com/mlafeldt/sharness/)Fork，并在那里发送拉动请求.

## 写测试

请看一下现有的测试,试着遵循他们的例子.

注意以下可能性,且不低的情况，这意味着大多数时候，ipfs 命令不应该在管道的左侧，因为如果 ipfs 命令失败(退出非零)，管道将 **屏蔽** 此失败。例如,在`false | true`,`echo $?`之后会打印 **0** (尽管`false`失败了).

应该把大部分代码放进去`test_expect_success`,或`test_expect_failure`块,并将这些块内的所有命令用`&&`链接，或`||`用于诊断命令.

### 诊断

使您的测试用例输出有助于，在 sharness 详细运行时。这意味着确定某些文件,或者运行诊断命令.例如:

```
test_expect_success ".ipfs/ has been created" '
  test -d ".ipfs" &&
  test -f ".ipfs/config" &&
  test -d ".ipfs/datastore" &&
  test -d ".ipfs/blocks" ||
  test_fsh ls -al .ipfs
'
```

这个`|| ...`就是前面命令失败时的一个诊断运行。`test_fsh` 是一个 shell 函数，它 echo 出参数，运行 cmd,然后也会失败，为了确保测试用例失败。(不希望诊断意外返回 true,使它 _看起来_ 像测试用例成功一样!.

### 对守护进程或安装命令进行测试

使用`lib/test-lib.sh`所提供的函数，运行守护进程或挂载:

要初始化,运行守护进程,一次挂载:

```sh
test_launch_ipfs_daemon_and_mount

test_expect_success "'ipfs add --help' succeeds" '
  ipfs add --help >actual
'

# 这里的其他测试......

# 别忘了杀死守护进程!!
test_kill_ipfs_daemon
```

要初始化,运行守护进程,然后单独挂载:

```sh
test_init_ipfs

# 测试但没有在这里运行

test_launch_ipfs_daemon

# 测试运行但未安装在此处

test_mount_ipfs

# 测试安装在这里

# 别忘了杀死守护进程!!
test_kill_ipfs_daemon
```
