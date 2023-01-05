---
title: "SpaceVim cscope layer"
description: "Слой cscope предоставляет умный помощник cscope и pycscope для SpaceVim, помогая пользователям выиграть в cscope"
---

# [Available Layers](../) >> cscope

<!-- vim-markdown-toc GFM -->

- [Intro](#intro)
- [Install](#install)
  - [cscope](#cscope)
  - [layer](#layer)
- [Layer options](#layer-options)
- [Key bindings](#key-bindings)

<!-- vim-markdown-toc -->

## Intro

Этот слой предоставляет интеллектуальный помощник [Cscope](http://cscope.sourceforge.net/) и [PyCscope](https://github.com/portante/pycscope) для SpaceVim.

Для получения дополнительной информации о различиях между Cscope и другими подобными инструментами, пожалуйста, прочитайте [Сравнение с аналогичными инструментами](https://github.com/oracle/opengrok/wiki/Comparison-with-Similar-Tools)

## Install

### cscope

```shell
sudo pacman -S cscope
```

В Windows вы можете использовать scoop для установки cscope:

```
scoop install cscope
```

### layer

Чтобы использовать этот уровень конфигурации, добавьте его в файл конфигурации.

```toml
[[layers]]
    name = "cscope"
```

## Layer options

- `cscope_command`: задайте команду или путь к исполняемому файлу `cscope`.
- `auto_update`: enable/disable автоматическое удаление при сохранении файлов.
- `open_location`: enable/disable откройте список местоположений после поиска.
- `preload_path`: установите пути предварительной загрузки.
- `list_files_command`: задайте команде список всех файлов, которые должны быть
задействованы для создания базы данных cscope, по умолчанию это:
  ```
  ['rg', '--color=never', '--files']
  ```
  Для определенных типов файлов используйте пользовательскую команду, например:
  ```
  [[layers]]
      name = 'cscope'
      list_files_command = ['rg', '--color=never', '--files', '--type', 'c']
  ```

## Key bindings

| Key Binding | Description                            |
| ----------- | -------------------------------------- |
| `SPC m c =` | Найдите присвоения этому символу        |
| `SPC m c i` | Создать cscope DB                       |
| `SPC m c u` | Обновить базы данных cscope                      |
| `SPC m c c` | Найдите функции, вызываемые этой функцией |
| `SPC m c C` | Найдите функции, вызывающие эту функцию   |
| `SPC m c d` | Найдите глобальное определение символа     |
| `SPC m c r` | найти ссылки на символ            |
| `SPC m c f` | найти файл                              |
| `SPC m c F` | найдите, какие файлы содержат файл        |
| `SPC m c e` | поиск по регулярному выражению              |
| `SPC m c t` | поиск текста                            |
