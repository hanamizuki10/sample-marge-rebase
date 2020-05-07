# sample-marge-rebase
Gitのrebaseとmergeの挙動の違いを検証

コミットメッセージ ルール
ブランチ名を記載する。


 - merge
 マージ、合流
 - fast-forward merge
 - non fast-forward merge
 - rebase

## ケース1.ブランチ branch-a を作成し、作業している最中にmasterの更新が発生

```
git checkout -b branch-a
git add README.md
git commit -m "branch-a, ブランチ作成とREADME更新"
git push origin branch-a
```

このあと、masterが更新されていると、知った。

### 対策としてmasterの内容をbranch-aへ適用させてみた。

#### 第一. master と競合していないか確認する。
現在の編集中の状況を全てコミットしてから master に切り替える。
git checkout master
git fetch
git merge origin/master