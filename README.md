# sample-marge-rebase
Gitのrebaseとmergeの挙動の違いを検証

コミットメッセージ ルール
ブランチ名を記載する。

 - merge
 マージ、合流
 - fast-forward merge
 - non fast-forward merge
 - rebase

## マスター用に追加
```
git clone git@github.com:hanamizuki10/sample-marge-rebase.git sample-marge-rebase-master
```

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
```
// いったんmasterブランチに切り替える
git checkout master
git fetch
// リモートとローカルのログを確認
git log
git log origin/master
// ソースコード差分を確認
git diff origin/master
// 問題ないためマージ
git merge origin/master
// ブランチをもとに戻す
git checkout branch-a
git fetch origin branch-a
// マスターと比較すると競合が発生している場合は-/+が表示される
git diff origin/master

// この状態で以下マージをするとCONFLICTが発生
git merge origin/master
//  > Auto-merging README.md
//  > CONFLICT (content): Merge conflict in README.md
//  > Automatic merge failed; fix conflicts and then commit the result.

// ステータスを確認すると以下のような表示になる
git status
//  > On branch branch-a
//  > You have unmerged paths.
//  >   (fix conflicts and run "git commit")
//  >   (use "git merge --abort" to abort the merge)
//  > 
//  > Unmerged paths:
//  >   (use "git add <file>..." to mark resolution)
//  > 
//  >         both modified:   README.md

// 競合したファイル README.md を修正し、以下のような感じでコマンド実行で適用させる
git add  README.md 
git commit -m "branch-a, 競合を解消"
```

### ケース1.ブランチ branch-a の内容をmasterにマージする
```
git fetch
git diff origin/branch-a
git merge origin/branch-a
// 競合を修正
git add  README.md 
git commit -m "master, ブランチbranch-aの内容をmasterにマージする,同時に競合を解消させる"
```
