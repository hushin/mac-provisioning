# mac-provisioning

[Mac の開発環境構築を自動化する (2015 年初旬編) - t-wadaのブログ](http://t-wada.hatenablog.jp/entry/mac-provisioning-by-ansible) を参考にした playbook です


## 使い方

### 準備

```
xcode-select --install
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew doctor
brew update
brew install python
brew install ansible

mkdir .mac-provisioning && cd $_
git clone git@github.com:hushin/mac-provisioning.git .
```

```
ansible-galaxy install --roles-path=. hnakamur.atom-packages
```

bash
```
echo 'export HOMEBREW_CASK_OPTS="--appdir=/Applications"' >> ~/.bash_profile
source ~/.bash_profile
```

zshで動かすとき
~/.zshrc あたりに追記
```
export HOMEBREW_CASK_OPTS="--appdir=/Applications"
export PATH=$HOME/.nodebrew/current/bin:$PATH
```

`source ~/.zshrc`

### 自動化開始


```
ansible-playbook -i hosts -vv localhost.yml
ansible-playbook -i hosts -vv frontend.yml
```

#### memo

すでにnodeをbrew install している場合は uninstall しておく
```
brew uninstall --force node
```

nodebrew で失敗するとき、 ~/.nodebrew/src のディレクトリを作ったらうまく行った

### TODO

- dotfilesなどリポジトリで管理したい
- playbook 一発で動くように書く
