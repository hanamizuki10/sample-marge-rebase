# sample-marge-rebase
Gitのrebaseとmergeの挙動の違いを検証

コミットメッセージ ルール
ブランチ名を記載する。

merge
fast-forward merge
non fast-forward merge
rebase

## マスター用に追加
```
git clone git@github.com:hanamizuki10/sample-marge-rebase.git sample-marge-rebase-master
```

branch-aの内容をmasterにマージする
```
git fetch
git diff origin/branch-a
git merge origin/branch-a
```
