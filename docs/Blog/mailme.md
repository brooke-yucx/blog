---
comments: true
---

MailMe 大法
===========

关于
----

* 标签：~blog
* 创建：2024-01-21

内容
----

通常有一些任务需要很久（几小时甚至几天）才能跑完，但中间如果出现错误跑不下去，没有及时处理的话会耽误很多时间。

这篇文章介绍的是一个在 Linux（Bash/Cshell）环境下使用邮件来通知一条 command 结束运行的方法，它来自我工作之后第一个项目的 customer~

目前这个方法我已经用在了很多项目，屡试不爽。因为最近又有人问起，总结一下，希望可以帮到有需要的朋友|･ω･｀)

### `mail` 和 `sendmail` 命令

`mail` 和 `sendmail` 是两个 Shell 工具，都可以用于发送邮件。用法如下：

* `mail`
    * 用法1
        * `echo "<content>" | mail -s <title> <receiver>`
    * 用法2
        * `mail -s <title> <receiver> < <content_in_file>`
* `sendmail` [20211012]
    * Bash：`(echo "From: <发件人>"; echo "To: <收件人>"; echo "Subject: <主题>"; echo "<第一行内容>" echo "<第二行内容>") | sendmail -t`
    * CShell：`echo "From: <发件人>\nTo: <收件人>\nSubject: <主题>.\n<第一行内容>\n<第二行内容>" | sendmail -t`

上述用法是我曾经用过的命令，可能也有更好写法，可以多探究一下~

### 用在脚本里

通常用在脚本里直接使用上述命令即可，通常可以把想要的信息放在主题和内容里，如放进一些环境变量和脚本里用到的变量等等。

至于如何在脚本中获得收件人地址，需要求助于跑脚本的环境，有些工作环境可能会有获得用户邮件的环境变量或 shell 工具；如果你确定用户环境中已经有 git 配置，可以调用 git config 里的邮件地址。

### 用在命令行里

如果不想把发邮件这个事情放在脚本里做？可以直接在命令行写，但命令很长，不如加个 alias。设置 alias 后，命令行里 `<一条想要得到完成通知的命令>; mailme &` 即可收到邮件。以 `sendmail` 为例：

* Bash：`alias mailme='(echo "From: <发件人>"; echo "To: <收件人>"; echo "Subject: <主题>"; time=$(date +\"%Y.%m.%d-%H.%M.%S\"); echo "Finished job at $time" echo "Directory: $PWD") | sendmail -t'`
    * 举例：`alias mailme='(echo "From: ${USER_MAIL}"; echo "To: ${USER_MAIL}"; echo "Subject: Job finished."; time=$(date +\"%Y.%m.%d-%H.%M.%S\"); echo "Finished job at $time"; echo "Directory: $PWD") | sendmail -t'`
* CShell：`alias mailme 'echo "From: <发件人>\nTo: <收件人>\nSubject: <主题>\n<第一行内容>\n<第二行内容>" | sendmail -t'`
    * CShell 可以在 alias 里加入参数，如在内容部分加入 `\!*.` 则可以在输入 `mailme test 001 is finished` 时在内容中收到 `test 001 is finished`
    * 举例：`alias mailme 'echo "From: ${USER_MAIL}\nTo: ${USER_MAIL}\nSubject: Job Finished.\nFinished job: \!*.\nDirectory: ${PWD}" | sendmail -t'`

### 注意事项

记得确认可以随时随地收到邮件提醒。

中断还是比轮询有效率很多吧！ᕕ(ᐛ)ᕗ
