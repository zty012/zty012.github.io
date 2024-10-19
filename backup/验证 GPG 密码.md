1. 将密码写入 `/tmp/p`，每行一个
2. 将任意内容写入 `/tmp/in`
3. 获取私钥 `gpg --list-secret-keys --keyid-format=long`
4. `for p in `cat /tmp/passphrases`; do echo "$p" | gpg -q --sign --local-user <secret> --passphrase-fd 0 --output /dev/null --yes /tmp/test.in && (echo "CORRECT passphrase: $p" && break); done`