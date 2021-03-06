---
title: GPG 使用
category: linux
tags: [gpg]
---

## 安装

```
brew update
brew search gpg
brew install gpg
```

### 帮助信息

`gpg --help`

### 生成密钥

`gpg --gen-key`

按提示填写资料后生成密钥对

#### 密钥回收

生成密钥对后应该立即做一个公钥回收证书，通过发布证书声明之前的公钥不再有效。

`gpg --output foo_revoke.asc --gen-revoke [uid]`

### 列出系统中已有密钥

`gpg --list-keys`

### 删除密钥

必须先删除私钥才能删除公钥

```
gpg --delete-secret-keys [uid]
gpg --delete-key [uid]
```

## 发布密钥到全球性的密钥服务器

`gpg --keyserver subkeys.pgp.net --send-keys [uid]`

### 导入密钥

```
gpg --import [密钥文件]
gpg --keyserver hkp://subkeys.pgp.net --search-keys [用户id]
# 无法保证服务器上的公钥是否可靠，下载后还需要其他机制验证。
gpg --fingerprint [uid] # 生成公钥指纹，在网站上公布，让其他人核对下载的公钥是否为真。
```

## 加密解密

```
gpg --recipient [加密的公钥] --output demo.en.txt --encrypt demo.txt
gpg --output demo.de.txt --decrypt demo.en.txt
```

## 签名与验证

### 生成未分离的签名文件

```
gpg --sign demo.txt
# 自动生成demo.txt.gpg文件，是签名后的二进制文件
gpg --clearsign demo.txt
# 自动生成demo.txt.asc文件，是签名后的ASCII文件
```

### 生成单独的签名文件

签名文件与文件内容分开存放

```
gpg --detach-sign demo.txt
# 生成单独的二进制签名文件demo.txt.sig
gpg --armor --detach-sign demo.txt
# 生成单独的ASCII签名文件demo
```

### 验证

```
gpg --verify demo.txt.asc # 验证未分离的签名文件
gpg --verify demo.txt asc demo.txt # 验证分离的签名文件
```

### 签名并加密

```
gpg --local-user [发信者id] --recipient [接收者id] --armor --sign --encrypt demo.txt
```

用decrypt解密即可，gpg会自动验证。

