# TCC Knowledge Database への貢献
## 提出に関する指針
### Issueの提出
[Issue Template](https://github.com/TCC-Study-Group/tcc-knowledge-database/issues/new/choose)に従ってください。

### プルリクエストの提出
プルリクエスト(PR)を提出する際は以下の指針を考慮してください。

1. このリポジトリを[Fork](https://docs.github.com/ja/github/getting-started-with-github/quickstart/fork-a-repo)する。
2. Forkしたリポジトリで以下のコマンドを使用してブランチを作る。
    ```
    git checkout -b my-fix-branch master
    ```
3. テストケースを作成する。
4. 変更を行う。
5. すべてのテストケースが通過するかを確認する。
6. [コミットメッセージの規約](#コミットメッセージの形式)に従ってコミットメッセージを記述し、以下のコマンドでコミットを行う。
    ```
    git commit --all
    ```
    注記: コマンドの`-a`オプションは、編集したファイルの`add`と`rm`を自動で行います。
7. 以下のコマンドでGitHubのあなたのリポジトリにPushする。
    ```
    git push origin my-fix-branch
    ```
8. GitHub上で`tcc-knowledge-database:develop`に対するPRを作成する。

#### コミットメッセージの編集
コミットメッセージが規約に従っていない場合は修正をする必要があります。

1. ブランチを変更する。
    ```
    git switch my-fix-branch
    ```
2. 直前のコミットを修正する。
    ```
    git commit --amend
    ```
3. GitHubのあなたのリポジトリにPushする。
    ```
    git push --force-with-lease
    ```

#### PRがMergeされたら
PRがMergeされた後はブランチを削除し、主流(upstream)のリポジトリからPullが行なえます。

- GitHubのWeb上で、またはコマンドでリモートリポジトリのブランチを削除する。
    ```
    git push origin --delete my-fix-branch
    ```

- mainブランチに変更する。
    ```
    git switch main -f
    ```

- ローカルのブランチを削除する。
    ```
    git branch -D my-fix-branch
    ```

- 最新のupstreamからmainブランチを更新する。
    ```
    git pull --ff upstream main
    ```

## コミットメッセージの形式
_これは[Angularのコミットメッセージ形式](https://github.com/angular/angular/blob/master/CONTRIBUTING.md#-commit-message-format)、及び[Angular.jsのコミットガイドライン](https://github.com/angular/angular.js/blob/master/DEVELOPERS.md#-git-commit-guidelines)を参考に制定しています。_

Gitのコミットメッセージの形式を厳密に制定します。これはコミットの可読性向上を目的としています。

コミットメッセージは、**Header**、**Body**、**Footer**から構成されます。
```
<Header>
<空行>
<Body>
<空行>
<Footer>
```

`Header`は必須項目であり、[コミットメッセージのHeader](#コミットメッセージのHeader)に準拠して記述する必要があります。

`Body`は`docs`タイプを除いたすべてのコミットで必須項目です。これを記述する場合、最低でも20文字程度の長さにしつつ[コミットメッセージのBody](#コミットメッセージのBody)に準拠して記述する必要があります。

`Footer`は任意項目です。[コミットメッセージのFooter](#コミットメッセージのFooter)に準拠して記述する必要があります。

### コミットメッセージのHeader
```
<タイプ>: <概要>
  │        │
  │        └─⫸ 概要。句読点は含まない。
  │
  └─⫸ コミットタイプ: build|ci|docs|feat|fix|perf|refactor|test
```
`タイプ`、`概要`ともに必須項目です。

#### タイプ
以下のいずれかを使用しなければなりません。

- feat: 新規機能の追加
- fix: バグ修正
- docs: ドキュメントのみの変更
- style: 内容の変更がないコードの変更 (空白、フォーマット、セミコロン抜けの修正など)
- refactor: バグ修正や新規機能の追加を行わないコード変更
- perf: パフォーマンス改善を目的としたコード変更
- test: テストの追加や既存テストの修正
- chore: ビルドプロセスやドキュメント生成などのライブラリ、補助ツールの変更 (依存ライブラリの追加なども含む)

#### 概要
概要には変更についての簡潔な説明を記述してください。

- 内容は体言止めで記述する。「変更しました」「変更する」ではなく「変更」
- 句読点は使用しない

### コミットメッセージのBody
ここではその変更に至った動機を記述してください。なぜこの変更を行ったのかなど。変更の影響の説明として以前の動作と新たな動作の比較する内容を含めても構いません。

### コミットメッセージのFooter
Footerには破壊的変更に関する情報などを記述します。またはこのコミットによってクローズ、または関連するGitHubのIssueやPRを指定したりすることも可能です。

```
破壊的変更: <変更に関する概要>
<空行>
<破壊的変更とそれに伴う移行についての説明>
<空行>
<空行>
#<Issue番号> を修正
```

## コミットの巻き戻し
コミットを戻す場合、コミットメッセージのHeaderは`revert:`で始まり、その後に戻すコミットのHeaderが続くようにしてください。

コミットメッセージのBodyには次のものを含むようにしてください。

- 戻すコミットのSHA情報。記述形式の例: `これはコミット <SHA> を戻します。`
- コミットを戻す理由