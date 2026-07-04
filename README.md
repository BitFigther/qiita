# qiita

qiitaの記事

## 記事を作るときの流れ

### 1. 記事ファイルを作成

```bash
npx qiita new 記事のファイル名
```

`public/記事のファイル名.md` が作成される。ファイル名はローカル管理用（URLにはならない）なので、内容がわかる英語名にする（例: `report-granularity`）。

### 2. プレビューしながら書く

```bash
npx qiita preview
```

http://localhost:8888 がブラウザで開く。ファイルを保存すると自動でプレビューに反映される。

### 3. 公開前チェック

フロントマターを確認する。

- `tags`: 1つ以上必須（最大5つ）
- `ignorePublish`: `false` にする（`true` のままだと公開対象外）
- `private`: 限定共有記事にする場合は `true`

### 4. コミット & プッシュで公開

```bash
git add public/記事のファイル名.md
git commit -m "記事タイトルなど"
git push
```

mainブランチへのpushをトリガーに、GitHub Actions（[.github/workflows/publish.yml](.github/workflows/publish.yml)）が自動で公開してくれる。

公開されるとフロントマターの `id` に記事IDが自動で入る（以降はこのIDで記事と紐づくため、ファイル名を変えてもOK）。

> [!NOTE]
> 記事IDの書き戻しはGitHub Actionsがリモートに直接コミットする。ローカルが古いままにならないよう、公開後や次の記事を書き始める前に `git pull` すること。

## その他のコマンド

| コマンド | 説明 |
| --- | --- |
| `npx qiita publish 記事のファイル名` | 手動で公開する（通常はpushに任せるので不要） |
| `npx qiita pull` | Qiita上の記事をローカルに取り込む（Web側で編集した場合の同期） |
| `npx qiita login` | アクセストークンを設定する（初回のみ） |
| `npx qiita version` | バージョン確認 |

## Tips

### 画像を貼りたい

Qiita CLIはローカル画像のアップロードに対応していない。
https://qiita.com/settings/uploading_images に画像をドラッグ&ドロップしてURLを発行し、`![説明](URL)` で貼る。


