# sample-marge-rebase
Gitのrebaseとmergeの挙動の違いを検証

コミットメッセージ ルール
ブランチ名を記載する。


 - merge
 - fast-forward merge
 - non fast-forward merge
 - rebase

## ケース1.ブランチ branch-a を作成し、作業している最中にmasterの更新が発生
git checkout -b branch-a
git commit -m "branch-a, ブランチ作成とREADME更新"
