# mac-provisioning

[Mac の開発環境構築を自動化する (2015 年初旬編) - t-wadaのブログ](http://t-wada.hatenablog.jp/entry/mac-provisioning-by-ansible) を参考にした playbook です


## 使い方

先に https://github.com/hushin/dotfiles を設定しておく。

### 準備

```
xcode-select --install
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew doctor
brew update
brew install python
brew tap homebrew/versions
brew install ansible@1.9

mkdir .mac-provisioning && cd $_
git clone git@github.com:hushin/mac-provisioning.git .
```

```
ansible-galaxy install --roles-path=. hnakamur.atom-packages
```

### 自動化開始


```
ansible-playbook -i hosts -vv localhost.yml
ansible-playbook -i hosts -vv frontend.yml
```

### Quick Look

Quick Lookで選択できるようにするコマンド
```
defaults write com.apple.finder QLEnableTextSelection -bool true && killall Finder
```

文字化け対策

```
cd ~/Library/QuickLook/QLColorCode.qlgenerator/Contents/Resources
sed -i -e 's|reader=(cat $target)|reader=(/usr/local\/bin/nkf -w -Lu $target)|' colorize.sh
```


#### memo

すでにnodeをbrew install している場合は uninstall しておく
```
brew uninstall --force node
```

nodebrew で失敗するとき、 ~/.nodebrew/src のディレクトリを作ったらうまく行った

### TODO

- playbook 一発で動くように 書く
