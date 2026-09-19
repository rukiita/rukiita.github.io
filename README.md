# rukiita.github.io

**GitHub Pages のユーザーサイト**（`https://rukiita.github.io/` のルートを提供する）。

## なぜこのリポジトリが要るのか

Google の OAuth 同意画面（Google Cloud Console）に利用規約・プライバシーポリシー・ホームページの URL を入れるには、
そのドメインを**「承認済みドメイン」に登録**する必要があり、登録には**Search Console での所有確認**が要る。

`github.io` は Public Suffix List に載っている共有ドメインなので、`rukiita.github.io` 自体が「トップ プライベート ドメイン」になる。
所有確認は Search Console の **URL プレフィックス プロパティ**＋**HTML ファイルのアップロード**で行うが、
そのファイルは**プロパティのルート**（`https://rukiita.github.io/<name>.html`）に置く必要がある。
`weird-config` は**プロジェクトサイト**で `/weird-config/` 配下しか提供しないため、ルートにファイルを置けず所有確認できない。

**ユーザーサイト（この `<ユーザー名>.github.io` という名前のリポジトリ）だけがルートを提供する。**
これを作ると `https://rukiita.github.io/` を自分で制御でき、所有確認 → 承認済みドメイン登録 → 同意画面の URL 入力が通る。

## 中身

| ファイル | 用途 |
|---|---|
| `index.html` / `index.en.html` | アプリのホームページ（日本語 / 英語）。Google の OAuth ポリシーは本番アプリに「アプリの機能の説明とプライバシーポリシーへのリンクを含む、公開されたホームページ」を求めており、これがそれに当たる |
| `google*.html` | ⚠️ **Search Console が発行する所有確認ファイル**（このリポジトリには含めない。Console からダウンロードしてここへ置く） |

法務文書（利用規約・プライバシーポリシー・サポート・アカウント削除）は**別リポジトリ `rukiita/weird-config` の `legal/`** にあり、
ここからは `/weird-config/legal/...` のリンクで参照している（**同じドメインなので承認済みドメインは 1 つで足りる**）。

## 作り方（初回）

1. GitHub で **`rukiita.github.io`** という名前の **public** リポジトリを作る（この名前でないとユーザーサイトにならない）
2. このディレクトリの中身を push する
3. Settings → Pages で `main` ブランチから配信されていることを確認する（数分かかる）
4. `https://rukiita.github.io/` が開くことを確認する

## Google の同意画面を公開するまで

1. [Search Console](https://search.google.com/search-console) で **URL プレフィックス**として `https://rukiita.github.io/` を追加
2. **HTML ファイル**の方法を選び、ダウンロードしたファイルをこのリポジトリのルートへ置いて push（数分待つ）
3. Search Console で「確認」を押す
4. Google Cloud Console → OAuth 同意画面 → **承認済みドメイン**に `rukiita.github.io` を追加
5. ホームページ `https://rukiita.github.io/`、プライバシーポリシー・利用規約の URL を入力して保存
6. 公開ステータスを「本番環境に公開」へ

⚠️ **アプリ内の法務リンク（`src/constants/legalUrls.ts`）とこのサイトは別物。** アプリ側は `weird-config` の URL を直接指しており、
このリポジトリを作っても変更は要らない。
