# siki-asar-releases

Siki の「Electron 非依存」配布物（`.asar`）を GitHub Releases の assets として配布し、リポジトリには `manifest.json`（インデックス）だけを置きます。stable/beta は「最新のみ」を保持し、履歴はタグ + Releases で管理します。

## 構成

- `manifest.json`: 利用可能なアプリバージョン一覧（エントリポイント）
- GitHub Releases assets: バージョンごとの `.asar`（例: `siki-0.1.0.asar`）

※ 旧運用の `app/` 配下は互換用の残置です（新フローでは参照しません）。

asar 内には、アプリ実行に必要な最小構成（例: `package.json`, `assets/main.js`, `assets/main_preload.js`, renderer 資産, `assets/`）のみを含めます。

## manifest.json（v3）

- 正式版（stable）/ ベータ版（beta）は、バージョン文字列が SemVer のプレリリースかどうか（例: `0.39.4-beta.1`）で判定します。
- `latest.stable` / `latest.beta` で、それぞれの最新版（バージョン文字列）を明示します。
- `apps[]` は、現在配布している stable/beta の「最新のみ」を列挙します（過去バージョンは保持しません）。
- `apps[].tag` と `apps[].asset` で GitHub Releases のタグ名・アセット名を指定します。

## 注意

- asar に Electron バイナリや `node_modules`、OS 依存ファイル、ビルドキャッシュは含めません。
