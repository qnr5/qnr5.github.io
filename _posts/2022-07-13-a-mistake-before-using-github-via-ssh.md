在配置git用ssh访问github时总是失败。猜测原因在于把验证文件填错名字了，生成了错误的日志，导致一直联不通。

github官方的ssh联通教程，轻微过一遍，就OK了。

ssh add ~/.ssh/id_rsa 这个命令简直救命了，它明示了要填正确的私钥。

用户名、邮箱随便设置不影响git clone工作。

有效命令如下：
```bash
$ ssh-keygen -t rsa -b 4096 -c "<your email>"
$ eval "$(ssh-agent -s)" 后台打开ssh-agent
$ ssh-add ~/.ssh/privatekey 添加私钥作为验证钥匙
```
接下来把公钥内容粘贴到github就好。
