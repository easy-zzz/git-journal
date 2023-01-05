---
title: "SpaceVim ctrlp layer"
description: "This layers provide a heavily customized ctrlp centric work-flow"
---

# [Available Layers](../) >> ctrlp

<!-- vim-markdown-toc GFM -->

- [Description](#description)
- [Install](#install)
- [Key bindings](#key-bindings)

<!-- vim-markdown-toc -->

## Description

Этот слой представляет собой сильно настроенную оболочку для [ctrlp](https://github.com/kien/ctrlp.vim ) (прекращено использование [этой вилки](https://github.com/ctrlpvim/ctrlp.vim ) вместо этого).

## Install

Чтобы использовать этот уровень конфигурации, добавьте его в свой файл конфигурации.

```toml
[[layers]]
	name = "ctrlp"
```

## Key bindings

| Key bindings         | Discription                   |
| -------------------- | ----------------------------- |
| `<Leader> f <Space>` | Fuzzy find menu:CustomKeyMaps |
| `<Leader> f p`       | Fuzzy find menu:AddedPlugins  |
| `<Leader> f e`       | Fuzzy найти регистр           |
| `<Leader> f h`       | Fuzzy find history/yank       |
| `<Leader> f j`       | Fuzzy найди прыжок, измени       |
| `<Leader> f o`       | Fuzzy найти контур            |
| `<Leader> f q`       | Fuzzy найдите быстрое решение          |
