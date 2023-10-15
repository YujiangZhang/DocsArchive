配置本地 ssh，设置别名

```bash
vim ~/.ssh/config
```

```plaintext
# 默认SSH密钥
Host github.com
HostName github.com
User git
IdentityFile ~/.ssh/id_rsa

# 另一个SSH密钥,github-other 是别名
Host github-other
HostName github.com
User git
IdentityFile ~/.ssh/id_rsa_other
```

克隆时

```bash
git clone git@[github-other]:username/repo.git
```

修改 URL

```bash
git remote set-url origin git@github-other:username/repo.git
```

