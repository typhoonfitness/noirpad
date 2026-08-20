# NoirPad — Support

A writing terminal for iPhone, iPad and Mac. If something is broken or you have
a question, this page is the place to start.

**Contact:** tylernoah070@gmail.com

Please include your device, your OS version, and the NoirPad version (it is on
the App Store page, and on Mac under NoirPad → About NoirPad). If something went
wrong while writing, a description of what you were doing right before it
happened helps more than anything else.

---

## Frequently asked

### Where are my notes stored?

On your device, and nowhere else. NoirPad has no account, no sync and no server.
Notes live in the app's own storage, and your preferences live in the standard
system preferences store. Deleting the app deletes them.

Anything you **Save** or **Export** goes wherever you choose in the file picker —
iCloud Drive, On My iPhone, a folder on your Mac, anywhere.

### I deleted a note by accident. Can I get it back?

Not from inside the app. Deleting a note asks for confirmation first and is
permanent. If you had saved or exported that note to a file, that file is
untouched — open it again with **Open**.

### What is the difference between Save and Export?

**Save** writes the note as a document you can reopen later. Choosing a `.html`
filename keeps all your formatting; choosing `.txt` writes plain text and drops
it. After the first save, Cmd-S (or Ctrl-S) writes straight back to that file.

**Export** produces a copy in another format for sending somewhere else — Word,
PDF, RTF, Markdown, JSON, CSV, teletype text, or a PNG screen capture. Export
never changes the note you are working on.

### Can I get my writing out if I stop using NoirPad?

Yes, and without any special tooling. Export as `.txt` or `.md` and you have a
plain file that opens anywhere. Nothing is locked in a proprietary format.

### The app is silent / too loud.

Typewriter sounds are a toggle: **FX → Writing → Sounds**. NoirPad plays through
the ambient audio channel and mixes with other apps, so it will not interrupt
music, and it respects the silent switch on iPhone.

### The effects make it hard to read.

Every effect is individually switchable under **FX**. Turn off Text glow, CRT
scanlines, Chromatic split and Phosphor bloom for the plainest possible page.
Weather and Scene both have an **Off** option.

### Typing feels slow on a long document.

Chromatic split is the most expensive effect, because it resamples the page as
you type. Turn it off first (**FX → Terminal → Chromatic split**), then Film
grain and Phosphor bloom.

### How do I use tables?

**▦ Table** on the format bar inserts one. Tap or click an existing table to open
its grid editor, where you can edit cells and add or remove rows and columns.

### Keyboard shortcuts

| | |
|---|---|
| Save | Cmd-S / Ctrl-S |
| Open | Cmd-O / Ctrl-O |
| Find | Cmd-F / Ctrl-F |
| New note | Cmd-Option-N |
| Bold / Italic / Underline | Cmd-B / Cmd-I / Cmd-U |
| Insert timestamp | F5 (Mac) · Cmd-Shift-T (iPad) |
| Zen mode | F9 (Mac) · Cmd-Shift-Z (iPad) |
| Leave Zen / close Find | Esc |

On iPhone and iPad these need a hardware keyboard. Everything is also reachable
from the toolbars and the **⋯** menu.

### Where did the toolbar go on my iPhone?

On a narrow screen the toolbar collapses to one row and the rest moves into the
**⋯** menu — New, Open, Save, Find, Export, Ink, Font and Text Size. Turn the
phone to landscape, or use an iPad or Mac, for the full bar.

### Zen mode hid everything and I cannot get out.

Press **Esc**, or F9 on a Mac. On a touch device without a keyboard, Zen mode is
toggled back off from where you turned it on — but if you are stuck, force-quit
and reopen; Zen mode is not remembered between launches.

---

## Reporting a bug

Open an issue on GitHub or send an email. Useful things to include:

- What you expected to happen, and what happened instead
- Whether it happens every time or only sometimes
- Your device and OS version
- A screenshot, if the problem is something you can see

## Requesting a feature

Very welcome. Tell me what you are trying to do rather than the feature you have
in mind — it is often the faster route to something that fits.

---

## Privacy

NoirPad collects nothing. See [PRIVACY.md](PRIVACY.md) for the full policy.
