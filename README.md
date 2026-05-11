# ghostty

Личный конфиг [Ghostty](https://ghostty.org) для macOS. Лежит в `~/.config/ghostty/`.

## Что внутри

- `config` — единственный конфиг Ghostty.
- `themes/` — симлинки на встроенные темы из бандла приложения (`Catppuccin Latte`, `Catppuccin Macchiato`).

## Основные решения

**Шрифт — [ALS Collimator VF](https://www.paratype.ru/fonts/pt/als-collimator)** (variable). Вес задаётся через ось `wght`, курсив — через ось `ital` (не `slnt`). Это важно: без явного `font-variation-italic = ital=12` italic визуально не отличается от regular — меняется только вес.

```
font-family = "ALS Collimator VF"
font-variation             = wght=400
font-variation-bold        = wght=900
font-variation-italic      = wght=400
font-variation-italic      = ital=12
font-variation-bold-italic = wght=700
font-variation-bold-italic = ital=12
```

Для нескольких осей ключ повторяется — `wght=400, ital=12` через запятую не работает.

**Тема** — Catppuccin, переключается по системной (`dark:Macchiato, light:Latte`).

**Окно** — нативный titlebar, opacity 0.95 + blur 20, padding 8×6.

**Клавиши** — навигация по вкладкам как в iTerm2 (`Cmd+←/→`, `Cmd+Shift+←/→`).

**Option** — `macos-option-as-alt = left`, чтобы правый Option продолжал работать для спецсимволов раскладки.

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
