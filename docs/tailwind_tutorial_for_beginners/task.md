# Tailwind UI 構築チュートリアル タスクリスト（3部構成・導入編の追加）

## プランニング
- [x] 「Tailwindの始め方」「Tailwindの哲学、コツ」「よくあるUIパーツの具体例」の3部構成へ改修する方針の策定

## UI実装 (`src/App.vue` 側の改修)
- [x] チュートリアルのデータ構造を「章（Chapter）」ベースへ大改修
  - `tutorialSteps` 配列をオブジェクト（`title`, `steps`）を内包する `tutorialChapters` 配列へ変更
- [x] 第1章：Tailwindの始め方（セットアップ編）の追加
  - Step 1: Vite + Tailwind v4 インストール（ターミナル風デモUI）
  - Step 2: Tailwind v4 有効化（VS Code風エディタデモUI）
- [x] 第2章：Tailwindの哲学、コツ（既存ステップの移行・調整）
  - Step 3〜8（旧Step1〜6）の内容を第2章へ格納
- [x] 第3章：よくあるUIパーツの具体例（Nordic Dark実践編）
  - Step 9〜11（旧実践1〜3）の内容を第3章へ格納
- [x] 画面テンプレート（`<template>`）の改修
  - 章のタイトル（例：「第1章」「第2章」）を大きく区切りとして表示する装飾UIの実装
  - v-for ループのネスト化（`v-for="chapter in tutorialChapters"` の中に `v-for="step in chapter.steps"`）

## 仕上げ・検証
- [x] 新規追加のデモ（ターミナル風／エディタ風）の表示と世界観が一致しているか確認
- [x] ローカル環境での挙動確認とWalkthrough更新
