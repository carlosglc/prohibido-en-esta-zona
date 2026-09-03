# Sticker Notebook

A notebook for tracking a program that comes in stages. You check off what you finish, keep a list of what you actually produced along the way, and give yourself an honest score from 0 to 100. Every stage you close gets stamped, and the board at the top shows you where you stand at a glance.

It works for anything shaped like "N steps": a 16-week course, a 30-day challenge, a 24-chapter book, a training block.

> The interface is in Spanish. Every string lives in one object in the source, so translating it is a single edit — see [Customizing](#customizing).

## How to use it

1. Open the page.
2. If you've opened a notebook before, it's listed at the top — click it to pick up where you left off.
3. Otherwise type what you're tracking, pick what it's measured in (weeks, days, modules, sessions or chapters) and how many, then hit **Crear libreta** (create notebook).

From there, for each stage you can:

- **Mark it done** with the checkbox on the left. That's what puts the stamp on the board.
- **Name it and date it** by typing directly over the text.
- **List deliverables** — the problem set, the run, the chapter — and tick them off individually.
- **Score yourself 0 to 100** with the slider. The color runs from red to green as it climbs.
- **Leave notes** about what got stuck and what went well.

There's no save button. Everything is written as you type.

## Sound

Every action has its own sound: an ascending chord when you stamp a stage, a blip when you tick off a deliverable, and the score slider plays a pentatonic scale that rises as you rate yourself higher.

None of it is audio files. It's synthesized on the spot with Web Audio, so it weighs nothing and there's nothing to download. Browsers won't let anything play until the user clicks, so the page will never startle anyone on load.

The **sonido** button in the header turns it off and remembers your choice.

## Where your data lives

In your browser, and nowhere else. No account, no server, nobody else can see what you write. That has two consequences worth being clear about:

- If you clear your browser data, the notebook goes with it.
- It doesn't sync between your laptop and your phone. Those are separate notebooks.

That's what the **Descargar respaldo** (download backup) and **Cargar respaldo** (load backup) buttons are for. The backup is a `.json` file you can keep anywhere and reload in another browser.

## The buttons at the bottom

| Button | What it does |
|---|---|
| Copiar resumen en Markdown | Copies your progress, already formatted, ready to paste into a blog post or a doc |
| Descargar respaldo | Downloads a `.json` with everything |
| Cargar respaldo | Restores from a `.json` |
| Copiar link de esta libreta | Copies the URL holding your configuration |
| Empezar otra | Opens a new notebook without erasing the current one |

## Running several notebooks

The configuration lives in the URL. A link like this:

```
.../?t=Run%2010K&u=semanas&n=12
```

opens the "Run 10K" notebook over 12 weeks. A different link with a different topic opens a separate notebook with its own progress stored independently, and every notebook you open gets listed on the cover page so you can get back to it without the link.

The parameters are:

- `t` — the topic
- `u` — `semanas`, `dias`, `modulos`, `sesiones` or `capitulos`
- `n` — how many stages

## Publishing it

It's a single HTML file with no dependencies and no build step. Any static file host will do.

With **GitHub Pages**, which is free and requires installing nothing:

1. Put `index.html` at the root of a public repo.
2. In the repo, go to **Settings → Pages**.
3. Under *Source* pick **Deploy from a branch**, branch `main`, folder `/ (root)`.
4. Save. In a couple of minutes it'll be live at `https://<your-user>.github.io/<your-repo>/`.

It also works if you just download `index.html` and double-click it. It opens in your browser with no internet.

## Customizing

Everything is in the same file:

- **Interface text** is collected in the `T` object near the top of the script. Change those lines and you've translated the whole app.
- **Units and durations** live in the `UNITS` object. That's where you add your own menu options.
- **The stamps** are eight SVGs in the `STAMPS` array. Swap them for whatever you like. They cycle by position, so a program longer than eight stages will reuse them.
- **Colors** are CSS variables at the top of the `<style>` block.
- **The scoring scale** is in the `scoreColor` function. The current breakpoints are 50, 60, 70, 80 and 90.
- **Sounds** are in the `SND` module. Each one is a short list of frequencies — change the notes, or set `master.gain` lower if you want it quieter.

## Technical notes

No frameworks, no bundler, no `node_modules`. HTML, CSS and JavaScript in one file. The only external thing is the M PLUS Rounded 1c typeface from Google Fonts, and if it fails to load it falls back to the system rounded font.

It saves with `localStorage`. If the file is opened inside a Claude artifact it uses `window.storage` instead; the same file works in both contexts.
