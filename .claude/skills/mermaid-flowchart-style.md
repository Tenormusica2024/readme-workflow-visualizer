# Mermaid Flowchart Style Guide

## Overview
GitHub READMEにMermaidフローチャートを作成する際の標準スタイルガイド。
パステルカラー + カラフル枠線でモダンなデザインを実現。

## When to Apply
- 「フローチャートを作って」
- 「ワークフローを可視化して」
- 「Mermaidで図を作成して」
- READMEにシステム構成図を追加する時

## Standard Template

```mermaid
%%{init: {'theme': 'neutral', 'themeVariables': { 'fontSize': '14px', 'fontFamily': 'system-ui'}}}%%
flowchart TB
    subgraph MAIN["メイングループ"]
        direction TB
        A([Start]):::mint --> B[処理1]:::lavender
        B --> C{判定}:::butter
        C -->|Yes| D[成功処理]:::sage
        C -->|No| E[エラー処理]:::coral
        D --> F[次の処理]:::sky
        E --> F
        F --> G[完了]:::mint
    end

    classDef mint fill:#ECFDF5,stroke:#6EE7B7,stroke-width:2px,color:#047857
    classDef lavender fill:#F5F3FF,stroke:#C4B5FD,stroke-width:2px,color:#6D28D9
    classDef periwinkle fill:#EEF2FF,stroke:#A5B4FC,stroke-width:2px,color:#4338CA
    classDef butter fill:#FFFBEB,stroke:#FCD34D,stroke-width:2px,color:#B45309
    classDef coral fill:#FFF1F2,stroke:#FDA4AF,stroke-width:2px,color:#BE123C
    classDef sky fill:#F0F9FF,stroke:#7DD3FC,stroke-width:2px,color:#0369A1
    classDef rose fill:#FFF1F2,stroke:#F9A8D4,stroke-width:2px,color:#BE185D
    classDef peach fill:#FFF7ED,stroke:#FDBA74,stroke-width:2px,color:#C2410C
    classDef lilac fill:#FAF5FF,stroke:#D8B4FE,stroke-width:2px,color:#7E22CE
    classDef silver fill:#F9FAFB,stroke:#9CA3AF,stroke-width:2px,color:#374151
    classDef sage fill:#F0FDF4,stroke:#86EFAC,stroke-width:2px,color:#15803D
    classDef blush fill:#FDF2F8,stroke:#F9A8D4,stroke-width:2px,color:#9D174D
    classDef cloud fill:#F0F9FF,stroke:#93C5FD,stroke-width:2px,color:#1D4ED8
```

## Color Palette Reference

| Class | Fill (背景) | Stroke (枠線) | Text (文字) | Usage |
|-------|------------|---------------|-------------|-------|
| mint | #ECFDF5 | #6EE7B7 | #047857 | 開始/終了/成功 |
| lavender | #F5F3FF | #C4B5FD | #6D28D9 | 通常処理 |
| periwinkle | #EEF2FF | #A5B4FC | #4338CA | DB/データ処理 |
| butter | #FFFBEB | #FCD34D | #B45309 | 判定/分岐 |
| coral | #FFF1F2 | #FDA4AF | #BE123C | エラー/警告 |
| sky | #F0F9FF | #7DD3FC | #0369A1 | 出力/エクスポート |
| rose | #FFF1F2 | #F9A8D4 | #BE185D | Git操作 |
| peach | #FFF7ED | #FDBA74 | #C2410C | フラグ/マーカー |
| lilac | #FAF5FF | #D8B4FE | #7E22CE | AI/分析処理 |
| silver | #F9FAFB | #9CA3AF | #374151 | スキップ/無効 |
| sage | #F0FDF4 | #86EFAC | #15803D | 外部連携/API |
| blush | #FDF2F8 | #F9A8D4 | #9D174D | 分類結果 |
| cloud | #F0F9FF | #93C5FD | #1D4ED8 | ストレージ/DB |

## Design Principles

1. **テーマは `neutral`** - subgraph背景がクリーム系でノードが映える
2. **背景色は淡色 (95%+ 明度)** - 白に近いパステル
3. **枠線はTailwind 300番台** - 淡いが視認性のあるカラー
4. **stroke-width: 2px** - 枠線を少し太くして視認性UP
5. **フォントはsystem-ui** - 読みやすさ重視

## Node Shape Guidelines

- `([...])` - 開始/終了ノード (Stadium shape)
- `[...]` - 通常処理 (Rectangle)
- `{...}` - 判定/分岐 (Diamond)
- `[(...)...]` - データベース (Cylinder)
- `>...]` - 非対称 (Asymmetric)

## Example: Complex Workflow

```mermaid
%%{init: {'theme': 'neutral', 'themeVariables': { 'fontSize': '14px', 'fontFamily': 'system-ui'}}}%%
flowchart TB
    subgraph SCHEDULED["定期実行"]
        direction TB
        A([Start]):::mint --> B[データ収集]:::lavender
        B --> C{成功?}:::butter
        C -->|Yes| D[分類処理]:::lavender
        C -->|No| E[待機]:::coral
        E --> B
        D --> F[エクスポート]:::sky
        F --> G[Git Push]:::rose
    end
    
    subgraph MANUAL["手動処理"]
        direction TB
        H{フラグ確認}:::butter --> I[レビュー]:::lilac
        I --> J[AI分析]:::lilac
        J --> K[DB更新]:::periwinkle
    end
    
    G -.-> H
    
    classDef mint fill:#ECFDF5,stroke:#6EE7B7,stroke-width:2px,color:#047857
    classDef lavender fill:#F5F3FF,stroke:#C4B5FD,stroke-width:2px,color:#6D28D9
    classDef periwinkle fill:#EEF2FF,stroke:#A5B4FC,stroke-width:2px,color:#4338CA
    classDef butter fill:#FFFBEB,stroke:#FCD34D,stroke-width:2px,color:#B45309
    classDef coral fill:#FFF1F2,stroke:#FDA4AF,stroke-width:2px,color:#BE123C
    classDef sky fill:#F0F9FF,stroke:#7DD3FC,stroke-width:2px,color:#0369A1
    classDef rose fill:#FFF1F2,stroke:#F9A8D4,stroke-width:2px,color:#BE185D
    classDef lilac fill:#FAF5FF,stroke:#D8B4FE,stroke-width:2px,color:#7E22CE
```

## GitHub Limitations

- `background` themeVariable は無視される
- `mainBkg` も無視される
- グラデーションは未対応 (PR #5913 がマージされれば将来対応)
- Neo Look / Hand-Drawn Look は Mermaid Chart 専用

## Maintenance

フローチャートの定期更新時:
1. コードベースの変更を確認
2. フローチャートとの差異をチェック
3. 必要に応じて更新
4. README.mdを更新してcommit
