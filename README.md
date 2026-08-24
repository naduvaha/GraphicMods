# GraphicMods by Staili

[Русский](#русский) | [English](#english)

**Version / Версия:** `0.7.8`  
**Plugin / Плагин:** `GraphicMods.dll`  
**Для / For:** [Casualties: Unknown](https://store.steampowered.com/app/4576510/) Demo · Unity 2022.3 URP 2D

---

<a id="русский"></a>

<details open>
<summary><b>Русский</b></summary>

## Описание

Клиентский мод: передний план в духе Limbo, живее вода и свет, апскейл **NVIDIA DLSS** или **AMD FSR 1.0**, плюс **физика ощущений** (прыжок/ход своего тела, вода мира, сыпучий песок) с MP-синком клеток через KrokMP.  
Один DLL (+ native DLL только для DLSS). Массу предметов не меняет. NPC/мобов не патчит.

## Возможности

- **Передний план (Limbo)** — низкие кучи земли/скал/песка из ванильных тайлов перед игроком. Без деревьев и капсул.
- **Сортировка спрайтов** — тела и предметы ближе к камере рисуются «впереди».
- **Вода (графика)** — клон игрового `waterMat`, чуть сильнее отражение/пена.
- **Физика 0.6** — прыжок/ход/посадка только своего тела; buoyancy/drag/течения для всего мира; falling-sand (песок/гравий) на хосте/SP; dirty-cell пакеты жидкости/блоков в MP.
- **Свет** — volumetric-лучи, bloom, свет в полном разрешении.
- **Апскейл** — **Off / DLSS / FSR** + качество и шарп.
- **Брызги / обломки** — splash и debris VFX.

Параллакс задника отключён (щели чанков). Pixel Perfect не выключаем насильно.

## Физика (SP + MP)

| Что | Кто |
|-----|-----|
| Прыжок / ход / посадка | Только `PlayerCamera.main.body` (твой персонаж) |
| Плавучесть / drag / течения | Все тела в мире (одинаковые слайдеры у всех игроков) |
| Falling-sand | Хост или одиночка; гости получают дельты блоков |
| Жидкость CA | Ваниль на хосте; GraphicMods шлёт быстрые dirty-cell (34001/34002) поверх ванильного чанк-синка |

В мультиплеере **у всех должен быть GraphicMods 0.6+ и те же Physics-слайдеры**. Иначе вода/песок разойдутся. Предметы не утяжеляются. NPC не получают Jump/Move.

## Апскейл (DLSS / FSR)

В настройках: **Upscaler** = `Off` | `DLSS` | `FSR`, плюс **Quality** и шарп.

| Backend | Что делает | Нужно |
|---------|------------|--------|
| **DLSS** | NVIDIA Super Resolution | RTX + `NVUnityPlugin.dll` + `nvngx_dlss.dll` рядом с exe |
| **FSR** | URP FidelityFX FSR 1.0 | Любой GPU |
| **Off** | `renderScale = 1` | — |

## Установка

1. **BepInEx 5.4.x** в папке игры.
2. `GraphicMods.dll` → `BepInEx\plugins\`.
3. Для DLSS: папка `Native\` рядом с dll (мод скопирует к exe) или вручную в корень игры.
4. Запуск. В логе:
   ```
   Loading [GraphicMods by Staili 0.6.0]
   GraphicMods by Staili v0.6.0 loaded
   ```
5. Меню **Настройки → Mods → GraphicMods** с **QoL.Unknown**, иначе `BepInEx\config\staili.casualties.graphicmods.cfg`.

REQ:
https://www.nexusmods.com/scavprototype/mods/341
https://www.nexusmods.com/scavprototype/mods/7

## Если «не работает»

- Нет `Loading [GraphicMods…]` → dll не там / нет BepInEx / файл заблокирован Windows.
- Нет вкладки → нужен QoL; сам мод уже может работать.
- `Failed to load` / NVIDIA → поставь **FSR** (0.5.3+ не падает без NVIDIA).
- Demo и полная игра — один `CasualtiesUnknown.exe`; 0.6.0 грузится на обоих именах процесса.

## Конфиг (физика)

| Ключ | По умолчанию | Смысл |
|------|----------------|--------|
| `Physics.Enabled` | `true` | Мастер физики |
| `Physics.JumpMult` | `1.08` | Прыжок (локально) |
| `Physics.MoveMult` | `1.08` | Ход (локально) |
| `Physics.LandingStick` | `0.88` | Сцепление посадки |
| `Physics.WorldBuoyancy` | `1.1` | Плавучесть мира |
| `Physics.WorldDrag` | `1.05` | Сопротивление воды |
| `Physics.CurrentStrength` | `1.15` | Течения |
| `Physics.FallingSand` | `true` | Песок + гравий осыпаются |
| `Physics.FallingSandSoilClay` | `false` | Также глина/почва |
| `Physics.FluidSyncBoost` | `true` | MP dirty-cell + доп. симуляция на хосте |

## Совместимость

- KrokMP не обязателен (SP работает локально). В MP желателен одинаковый GraphicMods у всех.
- Не меняет массу предметов, коллайдеры блоков, AI NPC.
- Ванильные чанки 10153/10154 остаются страховкой.

## Содержимое релиза

| Файл | Куда |
|------|------|
| `GraphicMods.dll` | `BepInEx\plugins\` |
| `Native\NVUnityPlugin.dll` | корень игры (DLSS) |
| `Native\nvngx_dlss.dll` | корень игры (DLSS) |

</details>

---

<a id="english"></a>

<details>
<summary><b>English</b></summary>

## About

Client plugin: Limbo-style foreground, stronger water/light, **DLSS / FSR** upscale, plus **physics feel** (local jump/move, world water, falling sand) with MP dirty-cell sync via KrokMP.  
One DLL (+ native DLLs for DLSS only). Does **not** reweight items. Does **not** patch NPC/mob locomotion.

## Features

- **Foreground (Limbo)** — earth/rock/sand mounds from vanilla tiles.
- **Sprite depth sort**, **water material**, **lighting**, **upscale**, **splash/debris FX**.
- **Physics 0.6** — local body jump/move/landing; world buoyancy/drag/currents; host/SP falling sand (sand/gravel); MP dirty-cell fluid/block packets (34001/34002).

## Physics (SP + MP)

| What | Who |
|------|-----|
| Jump / move / landing | Local `PlayerCamera.main.body` only |
| Buoyancy / drag / currents | All bodies (same sliders on every peer) |
| Falling sand | Host or singleplayer; guests apply block deltas |
| Fluid CA | Vanilla on host; GraphicMods adds fast dirty-cell stream |

In multiplayer **everyone needs GraphicMods 0.6+ and the same Physics sliders**. Items are not reweighted. NPCs are not given Jump/Move patches.

## Install

1. BepInEx 5.4.x in the game folder.
2. Drop `GraphicMods.dll` into `BepInEx\plugins\`.
3. For DLSS: copy `Native\*.dll` next to the exe.
4. Launch → log shows `GraphicMods by Staili v0.6.0 loaded`.
5. Settings via QoL **Mods → GraphicMods** or the BepInEx config file.

REQ:
https://www.nexusmods.com/scavprototype/mods/341
https://www.nexusmods.com/scavprototype/mods/7

## Release contents

| File | Put it… |
|------|---------|
| `GraphicMods.dll` | `BepInEx\plugins\` |
| `Native\NVUnityPlugin.dll` | game root (DLSS) |
| `Native\nvngx_dlss.dll` | game root (DLSS) |

</details>
