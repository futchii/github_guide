# ローカルリポジトリを使う
## リポジトリとは
ファイルの変更履歴を含むバージョン管理に必要になる様々な情報を保持する場所をリポジトリと呼びます。  
ローカルリポジトリは手元のパソコン内に作成するリポジトリのことです。  
後ほど使いますがリモートリポジトリと呼ばれるリポジトリもあり、一般的には複数人で共有することを目的にサーバー上に作られます。  

## Gitで管理するファイルを作成する
### ワークツリーを作成する
ワークツリーはGitで管理したいファイルを配置するディレクトリのことです。  
本稿ではディレクトリは`git_learning`としホームディレクトリ直下に作成します。  
以下コマンドを用いることでディレクトリを作成する事ができます。  

```bash
~/ $ cd ~/
~/ $ mkdir git_learning
```    

### 管理するファイルを作成する
```bash
~/git_learning/ $ echo "#github learning" > README.md
```
上記コマンドで`#github learning`が書き込まれたファイルを作成することができます。  

## ローカルリポジトリを作成する
`git init`コマンドでローカルリポジトリを作成することができます。  
作業ディレクトリにローカルリポジトリが作成されるため`~/git_learning/`に移動してから実行してください。

ディレクトリの内容を確認できるコマンドに`ls`コマンドがあります。  
隠しファイルも表示するために`ls -a`を実行すると`.git`ディレクトリが確認できると思います。  
`.git`ディレクトリ内にGitが管理するデータが含まれるので削除しないよう気をつけてください。

## ローカルリポジトリの状態を確認する
`git status`コマンドを用いることでローカルリポジトリの状態を確認することができます。  
以下が`git status`の実行結果です。  
```~/git_learning/ $ git status
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        README.md

nothing added to commit but untracked files present (use "git add" to track)
```

### git statusの見方
`On branch master`  
masterブランチで作業していることを表します。ブランチについては、後ほど解説するので詳しくは割愛します。  
`No commits yet`  
一度もコミットしてない場合に表示されます。  
`Untracked files:`  
一度も管理対象になってないファイルを表示しています。  

## ファイルをコミットする
ファイルの変更履歴を保存することをコミットすると呼び、変更記録自体もコミットと呼びます。  
日時や変更したユーザーを含めたコミットには、コミットメッセージを付加することができます。コミットメッセージは、そのコミットで何を変更したのかを説明します。  

コミットする為にステージングと呼ばれる作業を行う必要があります。  
ステージングとは、ファイルの現在の状態を次のコミットに含めることです。  
ステージングされたファイル郡はステージングエリアに保存されます。  

次のコマンドを用いて`README.md`をステージングします。  
`git add README.md`  

ステージング後の変更はコミットに反映されないので注意してください。  

ステージングされたか`git status`コマンドを用いて確認してみましょう。以下のような表示に変わっていればステージングできています。  
```On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   README.md
```  


コミットする準備を終えたので、早速コミットしましょう。
`git commit -m "コミットメッセージ"`  
ここでは`初めてのコミット`をコミットメッセージにします。  

もう一度、`git status`を使って確認してましょう。  
```On branch master
nothing to commit, working tree clean
```  
これは全ての変更がコミットされ、ワーキングツリーとコミットに相違がないことをあらわしています。  

## ローカルリポジトリでの操作を取り消す
### ワークツリーの変更取り消す
ワークツリーの変更を取り消すには`git checkout`コマンドを使います。  

#### 一部のファイルだけ戻す場合
`git checkout -- <file>`

以下のように指定したディレクトリ以下を再帰的に戻すことも可能です。
`git checkout -- <directly>`  

`git checkout -- .`を作業ツリーのルートディレクトリで作業ツリー全体の変更を最後のコミットまで戻すことができます。  


#### 使ってみる
`README.md`を変更してから最後のコミットに戻します。

```bash
echo "## 変更部分" >> README.md
git checkout -- README.md
```
`echo`でREADME.mdに書き出されて`git checkout`で元に戻ったことが確認できたと思います。  

### ステージングを取り消す
ステージングを取り消すには`git reset`コマンドを使います。  

#### 一部のファイルだけステージングを取り消す場合
`git reset <file>`  

#### 全てのステージングを取り消す場合
`git reset`

ファイルを指定しなければ全てのステージングを取り消す事ができます。

#### 使ってみる
ひとまず、コミットしないファイルを作成し、ステージングします。  
```~/git_learning/ $ echo > ignore.md
~/git_learning/ $ git add ignore.md
```  
`git status`コマンドでステージングできた事を確認したら`git reset`コマンドを用いて取り消します。  
`git reset ignore.md`  
コマンド実行後、取り消せた事を`git status`で確認してください。  

以降必要ないので`rm ignore.md`で`ignore.md`は削除しましょう。  

### コミットを取り消す
#### 




[目次へ](../README.md)