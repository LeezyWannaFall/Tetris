# Tetris — консольная версия на C (ncurses)

![C](https://img.shields.io/badge/C-17A2B8?style=for-the-badge&logo=c&logoColor=white)
![Check](https://img.shields.io/badge/Check-4CAF50?style=for-the-badge)
![GCOV](https://img.shields.io/badge/GCOV-808080?style=for-the-badge)
![Makefile](https://img.shields.io/badge/Makefile-F05032?style=for-the-badge)
![ncurses](https://img.shields.io/badge/ncurses-6E5494?style=for-the-badge)

Консольный Tetris, разделённый на **библиотеку (логика игры)** и **CLI GUI (ncurses)**. Проект устроен модульно: движок можно протестировать отдельно, GUI подключается к библиотеке при линковке.

---

## Требования (зависимости)

Минимум:

* `gcc` (C11)
* `make`
* `ncurses` (dev)
  Доп. для тестов/покрытия/доки:
* `check` (фреймворк тестов)
* `lcov`, `gcov`, `genhtml`
* `doxygen`, LaTeX (`pdflatex` и пакеты, например `texlive-*`)
* `valgrind` (для отладки утечек)

На Debian/Ubuntu:

```bash
sudo apt update
sudo apt install build-essential gcc make libncurses-dev libcheck-dev lcov doxygen texlive-latex-extra valgrind
```

---

## Структура проекта (пример)

```
.
├─ brickgame/
│  └─ tetris/
│     ├─ s21_tetris.h
│     └─ s21_tetris.c
├─ gui/
│  └─ cli/
│     └─ gui.c
├─ tests/
│  └─ test.c
├─ Makefile
└─ README.md
```

* `brickgame/tetris` — логика (библиотека).
* `gui/cli` — интерфейс (ncurses).
* `tests` — тесты на check.
* `Makefile` — сборка/тесты/дока.

---

## Быстрый старт — сборка и запуск

Собрать библиотеку и бинарник:

```bash
make install
```

Запустить игру:

```bash
./tetris
```

Очистить артефакты:

```bash
make clean
```
Собрать библиотеку отдельно и потом линковать:

```bash
# собрать объект и архив библиотеки (пример)
make libtetris.a
# собрать GUI и линковать с библиотекой
make tetris
```

---

## Управление (по умолчанию)

* Влево: ← (KEY\_LEFT)
* Вправо: → (KEY\_RIGHT)
* Вниз (ускоренное падение): ↓ (KEY\_DOWN)
* Поворот: `w` / `W`
* Пауза: `p` / `P`
* Рестарт (после Game Over): `r` / `R`
* Выход: `q` / `Q`

(`gui/cli/gui.c` — там задаются точные клавиши.)

---

## Makefile — важные цели

Типичный набор целей, который должен быть у Makefile:

* `all` — собрать библиотеку и исполняемый файл (по умолчанию).
* `libtetris.a` — собрать статическую библиотеку с логикой.
* `tetris` — собрать GUI и линковать с библиотекой.
* `test` — собрать и запустить тесты (Check).
* `gcov_report` — собрать с флагами покрытия, запустить тесты, собрать lcov/genhtml отчёт.
* `dvi` — сгенерировать документацию через Doxygen + LaTeX (опционально).
* `clean` — удалить build-артефакты.

Пример вызова теста:

```bash
make test
```

Пример покрытия:

```bash
make gcov_report
# требует: lcov, genhtml, gcov
```

---

## Тестирование и пример теста

Запуск:

```bash
make test
```

---

## Документация (Doxygen)

1. Сгенерировать шаблон Doxyfile:

```bash
doxygen Doxyfile
xdg-open html/index.html   # открыть HTML
```

