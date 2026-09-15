# CLAUDE.md

このファイルは、Claude Code (claude.ai/code) がこのリポジトリで作業する際のガイドラインです。

## プロジェクト概要

task-board2 プロジェクト。React製のシンプルなタスクボードアプリ（タスクの追加・完了トグル・削除、localStorageへの永続化）。

## 技術スタック

- 言語 / ライブラリ: React 19
- ビルドツール: Vite 8（`@vitejs/plugin-react`）
- Lint: oxlint
- 状態管理: React標準の `useState` / `useEffect`（外部の状態管理ライブラリは未使用）
- データ永続化: ブラウザの `localStorage`（バックエンド・DBは未使用）
- 主要ディレクトリ / ファイル
  - `src/main.jsx` — エントリーポイント
  - `src/App.jsx` — ルートコンポーネント
  - `src/TaskBoard.jsx` / `src/TaskBoard.css` — タスクボード本体（機能コンポーネント）
  - `public/` — 静的アセット（favicon等）
  - `.github/workflows/deploy.yml` — GitHub Pagesへの自動デプロイ用CI
- 主なコマンド
  - `npm run dev` — 開発サーバー起動
  - `npm run build` — 本番ビルド（`dist/`に出力）
  - `npm run preview` — ビルド成果物のプレビュー
  - `npm run lint` — oxlintによる静的解析

## デプロイ先

- https://nchuujou-alt.github.io/task-board2/
- `main` ブランチへのpushをトリガーに GitHub Actions（`.github/workflows/deploy.yml`）がビルドし、GitHub Pagesへ自動デプロイする。
- Viteの `base` は `vite.config.js` でリポジトリ名に合わせて `/task-board2/` に設定済み。リポジトリ名を変更する場合はこの値も合わせて変更すること。

## コンポーネントの命名規約

- コンポーネントファイルは `PascalCase.jsx`（例: `TaskBoard.jsx`）とし、ファイル名とコンポーネント（default export）名を一致させる。
- コンポーネント専用のスタイルは同名の `PascalCase.css` を同じディレクトリに置き、コンポーネントファイル内で `import './ComponentName.css'` する（例: `TaskBoard.jsx` ⇔ `TaskBoard.css`）。
- コンポーネント内のイベントハンドラ関数は `addTask` / `toggleTask` / `deleteTask` のように「動詞 + 対象（camelCase）」で命名する。
- CSSクラス名はケバブケース（例: `task-item`, `task-form`, `empty-message`）を使用し、状態を表す修飾クラスは `done` のように短い単語を要素クラスに追加する形（`task-item done`）で表現する。
- 1ファイル1コンポーネントを基本とし、コンポーネントが肥大化してきたら関心事ごとに分割する。

## Git運用ルール

- **コードを変更するたびに、コミットしてGitHubへプッシュすること。** 変更を溜め込まず、意味のある単位（1機能・1修正など）ごとにこまめにコミット・プッシュする。
- コミットメッセージは変更内容が分かるように簡潔に記述する（日本語・英語どちらでも可、リポジトリ内で統一する）。
- プッシュ前に `git status` / `git diff` で差分内容を確認し、意図しないファイル（`.env` や認証情報など秘密情報を含むファイル）が含まれていないか確認する。
- 作業前に必ず最新の `main`（または既定のリモートブランチ）を取得してから作業を始める。
- force push（`git push --force`）や `git reset --hard` などの破壊的操作は、明示的にユーザーの許可を得た場合のみ行う。
- pre-commit / CI などのフックが失敗した場合は、フックを無効化（`--no-verify`等）するのではなく、原因を修正してからコミットし直す。
- リモートリポジトリ未設定の場合は、GitHub上にリポジトリを作成し、`origin` として登録した上で運用を開始する。

## 開発の進め方

- 実装は小さく区切り、動作確認できる単位でコミットする。
- 既存のコードスタイル・ディレクトリ構成に合わせる。
- テストやビルドが存在する場合は、コミット・プッシュ前に実行して壊れていないことを確認する。

## メモ

- このファイルはプロジェクトの成長に合わせて随時更新してください（技術スタック、セットアップ手順、テストコマンド、注意事項など）。
