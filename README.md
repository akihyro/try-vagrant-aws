VagrantでEC2インスタンスを構築してみる
======================================


構築手順
--------

### Vagrant インストール

```
$ wget https://dl.bintray.com/mitchellh/vagrant/vagrant_1.6.5_x86_64.rpm
$ sudo rpm -ivh vagrant_1.6.5_x86_64.rpm
```

### Vagrant プラグイン インストール

```
$ vagrant plugin install vagrant-aws
$ vagrant plugin install vagrant-omnibus
```

### AWSアクセスキー セット

```
$ export AWS_ACCESS_KEY_ID='{アクセスキーID}'
$ export AWS_SECRET_ACCESS_KEY='{シークレットアクセスキー}'
```

### SSH認証鍵 配置

```
$ cat ~/.ssh/try-vagrant-aws.pem
-----BEGIN RSA PRIVATE KEY-----
...
-----END RSA PRIVATE KEY-----
```

### インスタンス 構築/起動

```
$ vagrant up --provider=aws
```


インスタンス 操作手順
---------------------

### インスタンス 起動

```
$ vagrant up
```

### インスタンス 停止

```
$ vagrant halt
```

### インスタンス 破棄

```
$ vagrant destroy
```
