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
