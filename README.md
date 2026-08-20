# ghostty

Личный конфиг [Ghostty](https://ghostty.org) для macOS. Лежит в `~/.config/ghostty/`.

## Что внутри

Один файл — `config`. Темы берутся встроенные из бандла Ghostty, локальных копий не держим.

## Основные решения

**Шрифт — [Iosevka Nerd Font Mono](https://www.nerdfonts.com/font-downloads)**. Статический моноширинный с патчем Nerd Fonts (иконки для prompt'ов, file managers и т.п.).

```
font-family = "Iosevka Nerd Font Mono"
```

**Тема** — Catppuccin, переключается по системной:

```
theme = dark:Catppuccin Macchiato,light:Catppuccin Frappe
```

Обе встроены в Ghostty, ставить ничего не надо. Строка с Gruvbox оставлена закомментированной рядом — переключение обратно это правка одной строки.

**Окно** — нативный titlebar, opacity 0.95 + blur 20, padding 8×6.

**Клавиши** — навигация по вкладкам как в iTerm2 (`Cmd+←/→`, `Cmd+Shift+←/→`).

**Option** — `macos-option-as-alt = left`, чтобы правый Option продолжал работать для спецсимволов раскладки.

**Alt+стрелки** — шлются явными CSI-последовательностями:

```
keybind = alt+right=text:\x1b[1;3C
keybind = alt+left=text:\x1b[1;3D
keybind = alt+up=text:\x1b[1;3A
keybind = alt+down=text:\x1b[1;3B
```

Без этого правый Option на стрелках отдавал macOS-композицию (`ESC f` / `ESC b`), а zellij читал её как `Alt+f` и открывал ToggleFloatingPanes вместо перемещения по слову. `macos-option-as-alt = left` сам по себе не помогает: он про левый Option, а спецклавиши идут мимо него.

## Установка

```sh
git clone git@github.com:jtprogru/ghostty.git ~/.config/ghostty
```

Шрифт ставится отдельно — положить `.ttf` в `~/Library/Fonts/`.

## Полезные команды

```sh
ghostty +validate-config                          # тихо если ок
ghostty +show-face --string="Aa" --style=italic   # проверить, что Ghostty реально использует нужный face
ghostty +list-fonts | grep -i collimator          # доступные начертания
```

`+show-face` ловит молчаливый фолбэк на системный шрифт — если в `font-family` опечатка или указано имя именованного инстанса вместо семейства, Ghostty подставит другое без предупреждения.

## Что хотрелодится, а что нет

Большинство правок применяются по `Cmd+Shift+,` (reload config). `font-*`, `background-blur-radius` и оконные параметры требуют полного перезапуска (`Cmd+Q`).

## Ранее использовалось

### ALS Collimator VF

[ALS Collimator VF](https://www.paratype.ru/fonts/pt/als-collimator) — variable-шрифт студии Артемия Лебедева (ALS = Art. Lebedev Studio). Вес задаётся через ось `wght`, курсив — через ось `ital` (не `slnt`). Без явного `font-variation-italic = ital=12` italic визуально не отличается от regular — меняется только вес.

```
font-family = "ALS Collimator VF"
font-variation             = wght=400
font-variation-bold        = wght=900
font-variation-italic      = wght=400
font-variation-italic      = ital=12
font-variation-bold-italic = wght=700
font-variation-bold-italic = ital=12
```

Для нескольких осей ключ повторяется — `wght=400, ital=12` через запятую не работает. Веса: `400=Regular, 450=Book, 500=Medium, 600=Semibold, 700=Bold, 900=Black`.
