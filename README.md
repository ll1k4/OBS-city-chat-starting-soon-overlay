# Оверлей городского чата (City Chat Overlay)

Сцена «Скоро начнём» для OBS: город со сменой дня и ночи, из окон которого вылетают сообщения Twitch-чата в облачках из жидкого стекла. Один HTML-файл, без установки

**[English](#english) · [Русский](#русский)**
![Preview](https://github.com/ll1k4/OBS-city-chat-starting-soon-overlay/blob/main/1.gif)
<!-- После загрузки скриншота раскомментируй: ![Preview](preview.png) -->

---
## Русский

### Возможности

- **Реальное время суток.** Небо, солнце, луна, звёзды, закатное свечение и свет в окнах меняются по часам твоего ПК.
- **Чат в окнах.** Каждое сообщение из Twitch появляется в облачке с хвостиком, который указывает на окно, откуда оно «вылетело». Это окно подсвечивается.
- **Облачка из жидкого стекла.** Стекло преломляет и размывает город за собой. У каждого ника свой постоянный цвет и чёрная обводка, чтобы читалось на любом фоне.
- **Один файл.** Только `index.html`: без установки, сборки, аккаунтов и входа. Чат Twitch читается анонимно, только на чтение.
- **Безопасно.** Сообщения рисуются как текст на холсте, поэтому через чат нельзя внедрить HTML. Сообщения, начинающиеся с `!` (команды ботов), игнорируются.

### Быстрый старт (OBS)

1. Скачай `index.html` и положи в постоянное место, например `C:\OBS\city\index.html`.
2. В OBS открой сцену «Скоро начнём» → **Источники → + → Браузер**.
3. **Сними галочку «Локальный файл»** и вставь в поле **URL** (свой путь и свой канал):
   ```
   file:///C:/OBS/city/index.html?twitch=ТВОЙ_КАНАЛ
   ```
4. Размер: **ширина 1920, высота 1080**.
5. Включи **«Выключать источник, когда он не отображается»** и **«Обновлять браузер, когда сцена становится активной»**. Тогда страница не работает на других сценах и заново подключается к чату при каждом показе.

### Параметры в адресе

| Параметр | Пример | Что делает |
| --- | --- | --- |
| `twitch` | `?twitch=mychannel` | Канал Twitch, чат которого показывается. Без него чат не подключается. |
| `demo` | `?demo=1` | Тестовые сообщения из Twitch, YouTube и VK, чтобы проверить без эфира. |
| `hour` | `?hour=21` | Фиксирует время суток (0–24) вместо часов ПК. Удобно для предпросмотра. |
| `title` | `?title=Скоро%20вернусь` | Надпись сверху. `?title=` (пусто) скрывает её. |
| `ws` | `?ws=ws://127.0.0.1:8080` | Необязательно: читать сообщения из своего WebSocket (см. ниже). |

Параметры соединяются через `&`, например `?twitch=mychannel&hour=22`.

### YouTube, VK и другие чаты

Напрямую страница читает только Twitch. Для остальных платформ сообщения можно передать из любого агрегатора чатов или скрипта:

- **WebSocket:** `?ws=ws://127.0.0.1:ПОРТ`. Каждое сообщение должно быть JSON: `{"platform":"youtube","user":"Ник","text":"Привет"}`. Известные платформы (`twitch`, `youtube`, `vk`) получают свою метку и цвет.
- **JavaScript:** вызови `addChat('youtube', 'Ник', 'Привет')` на странице.

### Что стоит знать

- Нужен интернет (чат Twitch и шрифт Unbounded из Google Fonts). Без шрифта заголовок покажется системным шрифтом.
- Одновременно видно не больше шести облачков, остальные сообщения ждут в короткой очереди.
- Эффект стекла использует фильтры холста, поэтому нужен браузер на Chromium (Браузерный источник OBS подходит).
- Цвета, время жизни облачка и их число — обычные константы в скрипте, их легко поменять.

---
## English

### Features

- **Real time of day.** Sky, sun, moon, stars, sunset glow and lit windows follow your PC clock.
- **Chat in the windows.** Each Twitch message appears in a speech bubble with a tail pointing at the window it came from, and that window lights up.
- **Liquid-glass bubbles.** The glass refracts and blurs the city behind it. Each nickname gets its own stable colour, with a black outline so it stays readable on any background.
- **One file.** A single `index.html`: no install, no build step, no account, no login. It reads Twitch chat anonymously (read-only).
- **Safe.** Messages are drawn as canvas text, so chat cannot inject HTML. Messages starting with `!` (bot commands) are ignored.

### Quick start (OBS)

1. Download `index.html` and put it somewhere permanent, e.g. `C:\OBS\city\index.html`.
2. In OBS, open your "Starting soon" scene → **Sources → + → Browser**.
3. **Untick "Local file"** and paste this into **URL** (use your own path and channel):
   ```
   file:///C:/OBS/city/index.html?twitch=YOUR_CHANNEL
   ```
4. Set **Width 1920, Height 1080**.
5. Tick **Shutdown source when not visible** and **Refresh browser when scene becomes active**, so the page does not run on other scenes and reconnects to chat each time.

### URL parameters

| Parameter | Example | What it does |
| --- | --- | --- |
| `twitch` | `?twitch=mychannel` | Twitch channel whose chat is shown. Without it no chat is connected. |
| `demo` | `?demo=1` | Fake messages from Twitch, YouTube and VK, for testing without a stream. |
| `hour` | `?hour=21` | Fixes the time of day (0–24) instead of using the PC clock. Handy for previewing. |
| `title` | `?title=Be%20right%20back` | Text at the top. Use `?title=` (empty) to hide it. |
| `ws` | `?ws=ws://127.0.0.1:8080` | Optional: read messages from your own WebSocket (see below). |

Combine them with `&`, for example `?twitch=mychannel&hour=22`.

### YouTube, VK and other chats

The page reads Twitch directly. For other platforms, send messages in from any aggregator or script:

- **WebSocket:** `?ws=ws://127.0.0.1:PORT`. Each message must be JSON: `{"platform":"youtube","user":"Nick","text":"Hello"}`. Known platforms (`twitch`, `youtube`, `vk`) get their own label and colour.
- **JavaScript:** call `addChat('youtube', 'Nick', 'Hello')` from the page.

### Good to know

- You need an internet connection (Twitch chat and the Unbounded font from Google Fonts). Without the font the title falls back to a system font.
- At most six bubbles are shown at once, and extra messages wait in a short queue.
- The glass effect uses canvas filters, so it needs a Chromium-based browser source (OBS Browser Source is one).
- Colours, bubble lifetime and bubble count are plain constants in the script and easy to change.
