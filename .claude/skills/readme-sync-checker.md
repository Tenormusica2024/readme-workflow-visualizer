# README Sync Checker & Updater

## Overview
リポジトリのREADMEがコードベースと整合しているかチェックし、必要に応じて更新するSkill。
フローチャート追加の前提条件として実行される。

## When to Apply
- 「READMEを更新して」
- 「ドキュメントの整合性をチェックして」
- 「README最新化して」
- フローチャート追加を依頼された時（自動的に先行実行）
- 定期メンテナンス時

## Check Workflow

```
1. README.mdの現状把握
   ↓
2. コードベース分析
   ↓
3. 差異検出
   ↓
4. 更新提案/実行
   ↓
5. フローチャート追加（mermaid-flowchart-style.md参照）
```

## Step 1: README現状把握

以下の項目をREADMEから抽出:
- プロジェクト概要/説明
- インストール手順
- 使用方法/コマンド
- ディレクトリ構造
- 依存関係
- 設定ファイル
- API/エンドポイント一覧

## Step 2: コードベース分析

以下のファイルを確認:
- `package.json` / `requirements.txt` / `Cargo.toml` 等 → 依存関係
- `main.py` / `index.js` / `src/` 等 → エントリーポイント
- `.env.example` / `config/` 等 → 設定項目
- `scripts/` / `Makefile` 等 → 実行コマンド
- 最新のGitコミット → 最近の変更

## Step 3: 差異検出チェックリスト

### 必須チェック項目

| 項目 | チェック方法 | 重要度 |
|------|------------|--------|
| **依存関係** | package.json等 vs README記載 | HIGH |
| **インストール手順** | 実際に動作するか | HIGH |
| **コマンド一覧** | scripts vs README記載 | HIGH |
| **ディレクトリ構造** | 実ファイル vs README記載 | MEDIUM |
| **環境変数** | .env.example vs README記載 | MEDIUM |
| **バージョン情報** | 最新リリース vs README記載 | LOW |

### 差異の判定基準

**要更新（MUST FIX）:**
- 存在しないファイル/コマンドへの参照
- 動作しないインストール手順
- 削除された機能の説明が残っている
- 新機能がREADMEに未記載

**推奨更新（SHOULD FIX）:**
- ディレクトリ構造の不一致
- 依存バージョンの差異
- 古いスクリーンショット

**任意（NICE TO HAVE）:**
- 文章の改善
- 例の追加

## Step 4: 更新実行

### 更新フロー

```python
1. 差異レポート作成
2. ユーザーに確認（重要な変更の場合）
3. README.md更新
4. git diff で変更確認
5. コミット提案
```

### 更新時の注意事項

- **既存の構成を尊重** - セクション順序は変えない
- **追加は末尾** - 新セクションは適切な位置に
- **削除は慎重** - 不要と思われる情報も確認してから
- **日本語/英語の統一** - 既存の言語に合わせる

## Step 5: フローチャート追加

整合性チェック完了後:
1. `mermaid-flowchart-style.md` のスタイルを適用
2. メインワークフローを図示
3. 「システムワークフロー」セクションとして追加

## Auto-Execution Triggers

以下のコマンドで自動実行:

```
/readme-check [リポジトリパス]
```

または自然言語で:
- 「このリポジトリのREADMEを最新化して」
- 「ドキュメントとコードの整合性をチェックして」

## Output Format

### 差異レポート例

```markdown
## README整合性チェック結果

### MUST FIX (要修正)
- [ ] `scripts/old_command.py` は削除済みだがREADMEに記載あり
- [ ] インストール手順の `pip install -r requirements.txt` → `pip install -e .` に変更必要

### SHOULD FIX (推奨修正)
- [ ] ディレクトリ構造に `logs/` フォルダ追加
- [ ] 依存関係: twscrape 1.0 → 2.0 に更新

### フローチャート
- [ ] システムワークフロー図なし → 追加推奨

### 推奨アクション
1. 上記MUST FIXを修正
2. フローチャートを追加
```

## Integration with Other Skills

このSkillは以下と連携:
- `mermaid-flowchart-style.md` - フローチャート追加時に参照
- 将来的に `changelog-generator.md` 等と連携可能

## Limitations

- プライベートリポジトリは認証が必要
- 大規模リポジトリは分析に時間がかかる
- 自動修正は構造的な変更には限界あり
