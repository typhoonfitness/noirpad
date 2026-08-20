# NoirPad — native Swift

A full rewrite of the NoirPad HTML app as a native SwiftUI application. One
source tree builds for iPhone, iPad and Mac; there is no WebView, no HTML and
no JavaScript anywhere in the project.

## Building

Open `Noirpad.xcodeproj` and pick a destination. The single `Noirpad` target
now builds for both platforms:

- **iOS / iPadOS 26.5** — touch first, hardware-keyboard shortcuts supported.
- **macOS 26.0** — native AppKit, real menu bar, Open/Save panels.

Switch between them with the run destination popup. There is no second target
and no scheme to add; `SDKROOT` is `auto` and `SUPPORTED_PLATFORMS` covers
`iphoneos iphonesimulator macosx`.

## Layout

```
Noirpad/
  NoirpadApp.swift        entry point, macOS menu bar commands
  Core/
    Platform.swift        UIKit/AppKit typealiases, hex and font helpers
    Theme.swift           every look and preference, and the derived palette
    NoirAppModel.swift    document actions, session timer, schedulers
    NoteStore.swift       the notes drawer, autosave, persistence
    NoirAttributes.swift  list markers and the table attachment
    DocumentModel.swift   block model the exporters walk
  Editor/
    NoirTextHost.swift    the UITextView / NSTextView subclasses
    NoirEditor.swift      formatting, lists, tables, find and replace
    NoirEditorView.swift  the SwiftUI bridge
  Effects/
    CRTOverlays.swift     scanlines, grain, roll bar, interlace, curve, glitch
    WeatherLayer.swift    petals, snow, rain, storm, data rain, embers
    SceneLayer.swift      draws the pixel scenes
    Shaders.metal         chromatic aberration
    Scenes/               the six pixel-art scenes, ported cell for cell
  Export/                 html, doc, rtf, pdf, txt, teletype, md, json, csv, png
  Audio/NoirAudio.swift   synthesised typewriter clack and thunder
  UI/                     bars, popups, drawer, ContentView
```

## Notes on the port

**Rich text** is a real `NSTextStorage` rather than a `contenteditable`.
Bold, italic, underline and strikethrough are font traits and attributes;
bullet and numbered lists (with nesting) are a custom `noirList` attribute plus
a rendered marker, renumbered automatically after every structural edit.

**Tables** are a `NoirTableAttachment` that draws itself, because `NSTextTable`
is AppKit only. Tap or click a table to open its grid editor. The exporters
read the model directly, so tables survive into HTML, Markdown, CSV and RTF.

**Fonts.** The web version loaded Courier Prime and Special Elite from Google
Fonts. To keep the app free of network dependencies and bundled binaries, the
menu uses faces that ship with iOS and macOS — Courier New, Menlo, SF Mono,
Courier, American Typewriter, Times New Roman, Georgia and San Francisco. To
add Courier Prime, drop the `.ttf` into the `Noirpad` folder, add
`UIAppFonts` / `ATSApplicationFontsPath` to the generated Info.plist keys, and
add an entry to `NoirFontFamily.all`.

**Sound** is synthesised at runtime — a band-passed noise burst for the key
clack, a 1568 Hz sine for the carriage bell, and low-passed noise with a
swept filter for thunder. No audio files.

**Effects** are drawn by SwiftUI rather than CSS. The phosphor glow and bloom
are real `NSShadow` attributes on the text, so the caret and selection stay
crisp. Chromatic aberration is a stitchable Metal shader in `Shaders.metal`.

**macOS sandboxing** is on, with user-selected file access read/write, so Open
and Save work through the standard panels. Signing uses the existing team.

## Shipping

- `APPSTORE.md` — App Store Connect metadata, ready to paste, plus the App
  Privacy, age rating and export compliance answers.
- `SUPPORT.md` — the page behind the Support URL.
- `PRIVACY.md` — the page behind the Privacy Policy URL.

## The icon

Two designs, both black and white with the same phosphor bloom the app uses on
its text, and both drawn as solid white masses with the detail cut back out in
black so the silhouette survives down to a 16pt Finder icon.

- **`AppIcon`** — a spiral notepad, ruled. In use.
- **`AppIcon-Typewriter`** — the typewriter. Kept as an alternate.

To switch, change `ASSETCATALOG_COMPILER_APPICON_NAME` in the target's build
settings from `AppIcon` to `AppIcon-Typewriter`.

`Tools/make_icon.py` generates either set — the iOS 1024 in light, dark and
tinted, plus the macOS 16→512 ladder at 1x and 2x, with a matching
`Contents.json`. Below 64px each design switches to a simplified drawing with
fewer, chunkier parts so the small sizes do not turn to mush. Needs Pillow:

```
python3 Tools/make_icon.py notepad    AppIcon
python3 Tools/make_icon.py typewriter AppIcon-Typewriter
```

Run from `Noirpad/Assets.xcassets` (or pass a root) so it writes the sets in
place. The geometry lives in `draw_notepad` and `draw_typewriter`.
`NOTEPAD_SCALE` at the top controls how much of the tile the pad fills — lower
it for more black around the edge, raise it toward 1.0 to fill the tile.

There is also a pen that lies diagonally across the pad, switched off. Set
`DRAW_PEN = True` at the top of the script to bring it back; it is positioned
along its own axis, so `PEN_ANGLE` rotates it without disturbing anything else.
