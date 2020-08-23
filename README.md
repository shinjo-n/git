# git

## 基本的な開発運用フロー
1. リモートから特定のブランチを指定してcloneする
    - `$ git clone [リポジトリのアドレス] -b develop`

1. ベースブランチの確認
    - `$ git branch`

1. ベースブランチの状態確認
    - `$ git status`

1. ベースブランチを最新の状態へ更新
    - `$ git pull origin develop`

1. 作業ブランチ作成
    - `$ git checkout -b feature/add_top_page`

1. ベースブランチの確認
    - `$ git branch`

1. ___変更、テスト___

1. 変更内容を確認
    - `$ git status`

1. 全ての変更を追加
    - `$ git add -A`

1. コミットを1つにまとめる
    - `$ git rebase`

1. コミット
    - `$ git commit -m "refactor: Modify top page's message" -m "" -m "3行目"`
    - `--allow-empty` 空でコミット

1. リモートリポジトリへプッシュ（HEAD をつけると最新になる）
    - `$ git push origine HEAD`

---

1. Compage & pull request をクリック

1. close の後ろに isuu の番号か URL を入れる。

1. Create Pull Request ボタンをクリック

1. Squash and merge でマージするとプルリクの全てのMessageをまとめて１つのコミットにまとめる


----
1. ベースブランチの確認
    - `$ bit branch`

1. ベースブランチの状態確認
    - `git status`

1. ベースブランチを最新の状態へ更新
    - `git pull origin develop`





# ブランチを指定しない場合
git clone [リポジトリのアドレス]

1. ブランチを指定する場合
    - `git clone -b [ブランチ名][リポジトリのアドレス]`



1. GitHub の Issue に対応する作業ブランチを（MasterやDevelopブランチから）作成
    ブランチ名 ex:)
        Feature/<作業内容>
        Fix/<作業内容>

作業完了後
`$ git status` で変更したファイルの一覧を確認
`$ git diff` で差分を確認
`$ git add -A`
`$ git commit -m`
`$ git push origin HEAD` <- GitHub のリモートブランチへ Push
　ブランチ名を指定しなくてもカレントブランチをリモートへ Push が可能

Push したブランチからプルリクエストを作成
　テンプレートが有れば記入、レビューアーを指定
　プルリクのコメントに "close #Issue番号 (またはURL)" を入力で
　プルリクのマージで Issue も同時に Close される

差し戻しが有る場合は、ローカルで修正後に
`$ git add`
`$ git commi`t
`$ git rebase -i` ← コミットを１つにまとめる
`$ git push -f origin HEAD`

GitHub でOK ならプルリク画面でマージ をして完了

ローカルのマスターブランチを更新（作業前にもやる？）
`$ git checkout developer`
`$ git pull origin master`

別のブランチへ切り替える
`$git stash`

add commit を取り消す
`$ git reset`


## GitHub オプション
approve 機能、レビューアーの誰か一人が approve するまでマージ不可。
Automatically delete head branches で GitHub上の作業ブランチは自動で削除
Allow squash merging マージされる際には自動的にコミットが１つにまとめられる





## よく使われる略語
LGTM - "Looks Good To Me” 自分的にはOKだよ
SSIA - "Subject Says It All” タイトルがすべてを表している
TBD - "To Be Determined” あとで決める
TIA - "Thanks In Advance” 先にお礼を言います（手数かけるけど、よろしく）
TL;DR. - "Too Long. Didn't Read.” 長文なので、要約載せます
WFM - "Works For Me” 自分の手元ではうまくいく（自分にとって都合が良い）



## git
直前のコミットメッセージ修正
$ git commit --amend -m "cssを修正"

コマンドのコミットメッセージ改行
$ git commit -m "1行明" -m "[2行目（空行）]" -m "3行目"



コンフリクト修正

github 上で Pull request を作成した際にコンプリートが出た


リポジトリの変更 ← おおもと？
`$ git checkout develop`

リポジトリの更新取得
`$ git pull origin develop`

リポジトリの変更 ← 対象？
`$ git checkout feat/modify_readme`

git merge じゃないのは、余計なコミットが作成されてしまう。
`$ git rebase develop`

マージツール起動
`$ git mergetool`

ステータスで確認
`$ git status`

rebase で更新
`$ git rebase -continue`

ステータスで確認 ← ローカルの変更完了
`$ git status`

リベースを行ってるため "-f"
`$ git push -f origin HEAD`


## ブランチ説明

### masterブランチ
master ブランチは、Gitでリポジトリを新規作成するとデフォルトで作成されるブランチ。
master ブランチに直接コミットすることはなく、マージを行うだけ。

### developブランチ
develop ブランチは、開発の中心となるブランチ。
開発中は develop ブランチからブランチを切って、作業完了後に再びマージするという作業を繰り返す。
master ブランチ同様、直接このブランチにコミットすることはない。
リポジトリを新規作成したときに、master ブランチから develop ブランチを切っておきます。

### featureブランチ
feature ブランチは、機能の追加や変更、バグフィックスを行うブランチ。
ひとつの変更に対してひとつの feature ブランチを切ることになるため、開発中で最も使われるブランチ。
ブランチの名前は、変更の内容がすぐに分かるような名称にする。
develop ブランチから派生させ、作業完了後に再び develop ブランチにマージし
マージ完了後に削除するというのが一連の流れです。

### releaseブランチ
release ブランチは、その名の通り製品をリリースするために使うブランチ。
リリース作業は、develop ブランチから release ブランチを切って、そのブランチでリリース作業を行う。
リリース作業が完了したら、master ブランチと develop ブランチにマージして、
master ブランチのマージコミットにリリースタグ（バージョンなど）をつける。
その後、release ブランチは削除する。

### hotfixブランチ
そんなときには、master ブランチから直接 hotfix ブランチを切って緊急の修正を行います。
修正完了後に master ブランチと develop ブランチにマージして、リリースタグ（マイナーバージョンなど）をつけます。
その後、hotfix ブランチは削除します。派生元が master になるだけで、操作的には release ブランチと同様です。

### support ブランチ（オプション）
プロジェクトによっては不要ですが、旧バージョンをサポートし続けなければいけないプロジェクトでは support ブランチが必要です。
support ブランチでは、旧バージョンの保守とリリースを行います。
サポートが必要なバージョンの master ブランチのコミットから派生させ、サポートを終了するまで独立してバグフィックスやリリースを行います。


##
//	git に登録はするが、更新管理を行いたくない
`$ git update-index --skip-worktree [file]`
`$ git ls-files -v`


リモートの最新を取ってきておいて・・
`$ git fetch origin master`

ローカルのmasterを、リモート追跡のmasterに強制的に合わせる！
`$ git reset --hard origin/master`

すべて吹っ飛ぶ
git status でチェック git stash で保存など対応が必要

`$ git pull origin master`
は、
```$ git fetch origin master
$ git merge FETCH_HEAD
```

# git コマンド

## ローカルリポジトリの新規作成
$ git init

## リモートリポジトリをコピー
$ git clone <リポジトリ名>
$ $ git clone [リポジトリのアドレス] [[-b] ブランチ名]


## 変更履歴をステージに追加
$ git add [ファイル名]
$ git add [ディレクトリ名]
$ git add .

## 変更を記録する（コミット）
$ git commit
$ git commit -m "[メッセージ]" [-m "[メッセージ]"]
$ git commit -v


## 現在の変更状況を確認
$ git status

## 変更差分を確認（ワークツリーとステージの）
$ git diff
$ git diff [ファイル名]

## 変更差分を確認（ステージとリポジトリ）
$ git diff --staged


## 変更履歴を確認
$ git log

#### 一行で表示する
$ git log --oneline

#### ファイルの変更差分を表示する 
$ git log -p index.html

#### 表示するコミット数を制限する 
$ git log -n [コミット数]

## ファイルの削除を記録

#### ファイルごと削除
$ git rm [ファイル名]
$ git rm -r [ディレクトリ名]

#### ファイルを残したいとき （リポジトリを削除し、ワークツリーは削除しない）
$ git rm --cached [ファイル名]


## ファイルの移動を記録
$ git mv [旧ファイル] [新ファイル]



## リモートリポジトリ(GitHub)を新規追加
$ git remote add orign [リポジトリのアドレス]


## リモートリポジトリ(GitHub)へ送信
$ git push [リモート名] [ブランチ名] 
$ git push origin master


## コマンドにエイリアス
$ git config --global alias.ci commit 
$ git config --global alias.st status 
$ git config --global alias.br branch 
$ git config --global alias.co checkout



## 管理しないファイルをGitの管理から外す
.gitignore




# 変更を元に戻すコマンド

## ファイルへの変更を取り消す（ステージ → ワークツリー）
$ git checkout -- <ファイル名>
$ git checkout -- <ディレクトリ名>

## 全変更を取り消す(ステージ → ワークツリー)
$ git checkout -- .


## ステージした変更を取り消す （リポジトリ → ステージ 、 ワークツリー影響なし）
$ git reset HEAD <ファイル名>
$ git reset HEAD <ディレクトリ名>

## 全変更を取り消す （リポジトリ → ステージ 、 ワークツリー影響なし）
$ git reset HEAD .


## 直前のコミットをやり直す（リーカルリポジトリ）
$ git commit --amend



# GitHubとやり取りするコマンド

## リモートを表示する
$ git remote

## 対応するURLを表示
$ git remote -v


## リモートリポジトリを新規追加
$ git remote add [リモート名] [リモートURL]
ex:) $ git remote add tutorial https://github.com/user/repo.git

## リモートから情報を取得する （リモートリポジトリ → ローカルリポジトリ）
$ git fetch [リモート名]
$ git fetch origin

## リモートから情報を取得してマージ （リポジトリ → ローカルリポジトリ → ワークツリー）
$ git pull
$ git pull <リモート名> <ブランチ名>
$ git pull origin master

#### これは下記コマンドと同じこと
$ git fetch origin master
$ git merge origin/master



## リモートの詳細情報を表示
$ git remote show <リモート名>
$ git remote show origin


## リモートを変更・削除する
$ git remote rename <旧リモート名> <新リモート名>
$ git remote rename tutorial new_tutorial

$ git remote rm <リモート名>
$ git remote rm new_tutorial



# ブランチとマージのコマンド

## ブランチを新規追加（ブランチへの切り替えはしない）
$ git branch <ブランチ名>
$ git branch feature

## ブランチの一覧を表示
$ git branch

## 全てのブランチを表示する
$ git branch -a


## ブランチを切り替える
$ git checkout <既存ブランチ名>
$ git checkout feature

## ブランチを新規作成して切り替える
$ git checkout -b <新ブランチ名>


## 変更履歴をマージする（作業中のブランチにマージ）
$ git merge <ブランチ名>
$ git merge <リモート名/ブランチ名> 
$ git merge origin/master


## ブランチを変更
$ git branch -m <ブランチ名> 
$ git branch -m new_branch

## ブランチを削除（マージされてない場合は削除しない）
$ git branch -d <ブランチ名>
$ git branch -d feature

## 強制削除する
$ git branch -D <ブランチ名>



# リベースのコマンド

## リベースで履歴を整えた形で変更を統合する
$ git rebase <ブランチ名>

## プルのリベース型
$ git pull --rebase <リモート名> <ブランチ名>
$ git pull --rebase origin master
マージコミットが残らないから、 GitHubの内容を取得したい だけの時は --rebase を使おう


## プルをリベース型に設定
$ git config --global pull.rebase true

## masterブランチでgit pullする時だけ
$ git config branch.master.rebase true



## 複数のコミットをやり直す

$ git rebase -i <コミットID>
$ git rebase -i HEAD~3

 -i は --interactive の略
 
```
#やり直したいcommitをeditにする edit gh21f6d ヘッダー修正
pick 193054e ファイル追加
pick 84gha0d README修正
#やり直したら実行する
$ git commit --amend

#次のコミットへ進む(リベース完了)
$ git rebase --continue
```

# コミットを並び替える、削除する
$ git rebase -i HEAD~3
```
pick gh21f6d ヘッダー修正
pick 193054e ファイル追加
pick 84gha0d README修正

履歴は古い順に表示される。git logとは逆。


# 184gha0dのコミットを消す
# 2193054eを先に適用する
pick 193054e ファイル追加
pick gh21f6d ヘッダー修正
 コミットを削除したり 並び替えたりできる。
```

# コミットをまとめる
$ git rebase -i HEAD~3
```
pick gh21f6d ヘッダー修正
pick 193054e ファイル追加
pick 84gha0d README修正
↓
pick gh21f6d ヘッダー修正
squash 193054e ファイル追加
squash 84gha0d README修正

 squashを指定するとそのコミットを 直前のコミットと一つにする
```


# コミットを分割
$ git rebase -i HEAD~3
```
pick gh21f6d ヘッダー修正
pick 193054e ファイル追加
pick 41gha0d READMEとindex修正
↓
pick gh21f6d ヘッダー修正
pick 193054e ファイル追加
edit 84gha0d READMEとindex修正
```

$ git reset HEAD^
$ git add README
$ git commit -m 'README修正' $ git add index.html
$ git commit -m 'index.html修正' $ git rebase --continue


# タグ付けのコマンド

## タグの一覧を表示
git tag

```
# パターンを指定してタグを表示 
$ git tag -l "201705" 20170501_01
20170501_02
20170503_01

git tagコマンドはアルファベット 順にタグを表示
```


## タグを作成する(注釈付きタグ)
$ git tag -a [タグ名] -m "[メッセージ]"
$ git tag -a 20170520_01 -m "version 20170520_01"

```
-a オプションを付けると注釈付き タグを作成。
-m オプションを付けるとエディタを立ち上げずにメッセージを入力できる。

・名前を付けられる
・コメントを付けられる
・署名を付けられる
```


## タグを作成する(軽量版タグ)

$ git tag [タグ名]
$ git tag 20170520_01

## 後からタグ付けする
$ git tag [タグ名] [コミット名]
$ git tag 20170520_01 8a6cbc4

オプションを付けないと軽量版 タグを作成する。


## タグのデータを表示
$ git show [タグ名]
$ git show 20170520_01

タグのデータと関連付けられた コミットを表示する。

```
・タグ付けした人の情報
・タグ付けした日時
・注釈メッセージ
・コミット
 ```

## タグをリモートリポジトリに送信
$ git push [ブランチ名] [タグ名]
$ git push origin 20170520_01

## タグを一斉に送信する
$ git push origin --tags

 --tags を付けるとローカルにあって リモートリポジトリに存在しない タグを一斉に送信する。
 


# スタッシュのコマンド

## 作業を一次避難する
$ git stash
$ git stash save

stashは「隠す」という意味

ワークツリー、ステージ を退避


## 避難した作業を確認
$ git stash list

避難した作業の一覧を表示


## 避難した作業を復元

```
# 最新の作業を復元する
$ git stash apply

# ステージの状況も復元する
$ git stash apply --index

# 特定の作業を復元する
$ git stash apply [スタッシュ名]
$ git stash apply stash@{1}
```

## 避難した作業を削除

```
# 最新の作業を削除する
$ git stash drop

# 特定の作業を削除する
$ git stash drop [スタッシュ名]
$ git stash drop stash@{1}
# 全作業を削除する ~ $ git stash clear
```

## 独立した（共通の祖先が無い） Git リポジトリのマージ

1. ローカルでリポジトリを作成
   - `$ git init`
   - `$ git add -A`
   - `$ git commit -m "Initialize repository"`

1. GitHubでリポジトリを作成
   - "Initialize this repository with a README" にチェックを入れると後に conflict になる。

1. リモートリポジトリを追加
   - git remote add origin <GitHubリポジトリ>

1. ローカルリポジトリの変更をリモートレポジトリに反映
   - `$ git push origin master`

## 独立した（共通の祖先が無い） Git リポジトリのマージ

1. Conflict が起きた場合はマージする
   - `$ git merge --allow-unrelated-histories origin/master`
