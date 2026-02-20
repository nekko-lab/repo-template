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
