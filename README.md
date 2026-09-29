# Pass Preview Editor

**Design wallet tickets with confidence.**

The Pass Preview editor is a web tool for designing event tickets for Apple Wallet and Google Wallet. Fill in a form, see how the ticket will look on each platform, fix problems, and export ready-to-use JSON.

Live website: **(coming soon)**

> **Status: early development.** This README describes the v1 scope. Items marked *planned* are not built yet, see the [roadmap](#roadmap).

> Previews are approximations. Apple and Google do not publish pixel-exact rendering rules, and the result can differ by OS version. Always test on a real device before shipping.
>
> Pass Preview is not affiliated with Apple or Google.

---

## What it does

1. **Edit** the ticket in a form: event, venue, holder and seat, barcode, colours, images and extra fields.
2. **Preview** it live as an Apple Wallet or Google Wallet pass, side by side if you want, in the wallet's light and dark mode.
3. **Check** it. A warnings panel flags missing fields, low contrast, images with the wrong size or ratio, text that will likely be cut off, and values a platform does not support.
4. **Export** it as a set of JSON files you can hand to your backend.

Everything runs in your browser. There are no accounts and no uploads, and your projects are stored locally.

## Features (v1 scope)

- Event ticket pass type, previewed for Apple Wallet and Google Wallet
- Live preview with platform switch (Apple, Google, side by side), wallet light or dark mode and two device sizes
- Colour fields with hex input, picker and a live contrast ratio against the background
- Image fields for logo and banner, with recommended sizes and a size and ratio check
- Repeatable extra fields (key, label, value)
- Warnings panel with three severities (error, warning, info) and a "Go to field" action
- Import and export of a canonical `ticket.json`, plus a few example tickets, including one with deliberately awkward data
- Export dialog with a JSON viewer per file and a `.zip` download
- Dark UI with a scroll-driven globe scene, reduced-motion and low-power fallbacks

## Export

The export contains:

| File | Purpose |
|---|---|
| `ticket.json` | The canonical Pass Preview ticket. Re-import it to keep editing. |
| `apple/pass.json` | The `pass.json` for an Apple Wallet event ticket |
| `google/class.json` | Google Wallet event ticket class |
| `google/object.json` | Google Wallet event ticket object |

**The editor does not sign anything.**

## How the preview stays honest

- The preview is a hand-built approximation of each wallet, not a screenshot or an emulator.
- A permanent notice in the UI says so.
- The renderers are calibrated against screenshots from real devices, which are kept in the repo as fixtures. *(planned)*
- An optional overlay to compare the preview with your own device screenshot is planned.

If you spot a difference from a real device, please open an issue with a screenshot and the OS version.

## Tech stack

- [Next.js](https://nextjs.org) (App Router), React and TypeScript
- [Tailwind CSS](https://tailwindcss.com) with design tokens as CSS variables. All components are hand-built, with no component library.
- [framer-motion](https://www.framer.com/motion/) for the scroll-linked lighting

The globe and its lighting use CSS gradients, masks and transforms. No WebGL is involved.

## Project structure

```
apps/editor
├── app/                 # routes, layout, page (hero, editor, footer)
├── components/
│   ├── hero/            # globe scene and scroll-linked lighting
│   ├── editor/          # form sections, colour and image fields, extra fields list
│   ├── preview/         # preview controls and device frame
│   ├── warnings/        # warnings panel
│   └── export/          # export dialog, JSON viewer, zip
├── lib/                 # project state, local storage, examples, file import
└── styles/              # Tailwind config and design tokens
```

## Limitations

- Only the event ticket pass type is supported.
- Previews are approximations and are not verified on every OS version yet.
- No `.pkpass` signing, no Google Wallet API calls and no pass updates.
- No accounts, sync or collaboration. Projects live in your browser, so export `ticket.json` to keep a copy.
- Field mappings follow the public Apple and Google documentation. Please verify against the current docs and a real device, since both platforms change over time.

## Roadmap

- [ ] Reference fixtures from real iOS and Android devices
- [ ] Apple Wallet preview (classic event ticket)
- [ ] Google Wallet preview
- [ ] Warnings panel and "Go to field"
- [ ] Editor form, import and examples
- [ ] Export dialog and zip
- [ ] Hero and scroll-linked globe, with fallbacks
- [ ] Compare-with-screenshot overlay
- [ ] More pass types (loyalty, boarding pass, generic)

## Contributing

Issues and pull requests are welcome, especially:

- differences between the preview and a real device (please include a screenshot and the OS version),
- edge cases that should produce a warning,
- accessibility problems.

Please open an issue before starting a large change.

## License

[MIT](../../LICENSE). Apple, Apple Wallet, Google and Google Wallet are trademarks of their respective owners and are used here only to describe compatibility.
