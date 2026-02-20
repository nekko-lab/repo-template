# repo-template

NCチームで使用する開発環境のテンプレートです．

## セットアップ

### 1. ブランチ保護ルールの設定

`main` ブランチへの直接プッシュを禁止し，プルリクエスト経由のマージを強制します．

1. GitHub リポジトリの **Settings** > **Branches** を開く
2. **Add branch protection rule** をクリック
3. **Branch name pattern** に `main` / `master` を入力
4. 以下の項目を有効化し，**Save changes** をクリックする

| 設定項目 | 推奨値 | 説明 |
| --- | --- | --- |
| Require a pull request before merging | ✓ | マージ前に PR を必須にする |
| Require approvals | 1 以上 | 承認者の最低人数 |
| Require status checks to pass | ✓ | CI が通過しないとマージ不可 |
| Require branches to be up to date | ✓ | マージ前にベースブランチとの同期を必須にする |
| Include administrators | ✓ | 管理者にもルールを適用する |

---

### 2. 開発環境のセットアップ（Dev Container）

Dev Container を使用することで，チーム全員が同一の開発環境を再現できます．

#### 前提条件

- [Docker](https://www.docker.com/products/docker-desktop/) がインストール済みであること
- [Visual Studio Code](https://code.visualstudio.com/) がインストール済みであること
- VS Code 拡張機能 [Dev Containers](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers) がインストール済みであること

#### 手順

1. VS Code でリポジトリのルートディレクトリを開く
2. コマンドパレットを開く（`Cmd+Shift+P` / `Ctrl+Shift+P`）
3. `Dev Containers: Reopen in Container` を選択する
4. コンテナのビルドが完了するまで待つ

コンテナ起動後は，`.devcontainer/devcontainer.json` に定義された環境が自動的に適用されます．

---

### 3. チケット駆動開発のブランチ運用

GitHub Issues をチケットとして使用し，1 チケット 1 ブランチで作業を管理します．

#### ブランチ運用フロー

```
dev
 └─ feat/*** ─── 作業 ─── PR ──→ dev
```

1. GitHub Issues で `[FEAT]` チケットを作成する
2. `dev` ブランチから `feat/***` ブランチを切る（ブランチ名はチケットに記載）
3. `feat/***` ブランチで作業を行う
4. 作業完了後，`feat/***` から `dev` へ PR を作成してマージする

#### RACI

各チケットには以下の役割を記載します．**R はチケット作成者自身**が担います．

| 役割 | 説明 |
| --- | --- |
| R: 実行責任者 (Responsible) | 実際に作業を行う人．チケット作成者が担当する |
| A: 説明責任者 (Accountable) | 成果物に対して最終責任を持つ人 |
| C: 協業先 (Consulted) | 作業に際して相談・協力を求める人 |
| I: 報告先 (Informed) | 進捗・完了を報告する人 |
