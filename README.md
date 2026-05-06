[![CI](https://github.com/shirmanovak410-ops/lab04/actions/workflows/ci.yml/badge.svg)](https://github.com/shirmanovak410-ops/lab04/actions/workflows/ci.yml)

# lab04

Проект с настройкой непрерывной интеграции (CI) через GitHub Actions.

## Статус сборки

![CI Status](https://github.com/shirmanovak410-ops/lab04/actions/workflows/ci.yml/badge.svg)

## Сборка проекта

```bash
cmake -H. -B_build
cmake --build _build
./_build/example1
