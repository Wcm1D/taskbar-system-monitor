# Changelog

All notable changes to Taskbar System Monitor. Versions follow the
`@version` line in `taskbar-system-monitor.wh.cpp`.

## [1.1.0] - 2026-11

A UI/UX refactor of the settings window and the widget layout. Settings stay
in Windhawk's mod storage, nothing new goes online, and the Windhawk settings
page is unchanged.

### Presets
- Presets now save and apply the **layout style** and the **Primary zone
  alignment** (`primaryPin=auto|left`) along with the readings and look.
  Preset files from 1.0.0 still load; without a `primaryPin` line the
  current alignment is kept.
- Built-in presets retuned:
  - **Compact** (shown as Compact; stored key unchanged from Minimalist): one
    row with CPU and RAM joined, battery power hidden at zero, network, and
    weather by the clock.
  - **Balanced**: CPU with its temperature, RAM, GPU with its temperature,
    battery time with power, and network. Has no weather or ping, so a fresh
    install stays offline.
  - **Heavy Monitoring**: CPU and GPU with temperature and power, RAM and
    VRAM, fans, disk, download and upload, ping, with battery and weather by
    the clock.
  - Readings a PC may lack (battery, separate GPU, fans) are marked `?` and
    hide themselves.
- Presets popup: more space under headings, room for the scroll bar, and a
  one-line folder box with the full path in its tooltip.

### Auto-switch presets (Labs)
- New **Auto-switch** section in the Presets popup with three choices:
  **Default**, **On battery**, and **High load or fullscreen**. Each can be a
  built-in or saved preset.
- High load means CPU or GPU at 75% or more, ending below 65%. Fullscreen is
  any app Windows marks as fullscreen (games, video) or presentation mode.
- High load or fullscreen wins over battery. A change has to last 10 seconds
  before the preset switches, and a preset is only applied when the target
  changes.
- With **None (Manual)** as the default, your own setup is saved before the
  first switch and restored when the condition ends.
- Never switches while the settings window is open; edits made there are
  kept as the current state's setup.
- Runs on the existing sampling update: no new thread or timer. State is
  kept under `presets.auto.*` and cleared when all three rules are Off.

### Zones and layout
- New **Primary zone** replaces the Left and Center zones. It sits at the far
  left while Start is centered and in the middle while Start is aligned left.
  **Position ▸ Primary zone** can pin it to the far left.
- Existing `left:` and `center:` setups move into the Primary zone
  automatically, once.
- **Auto-compact**: when the taskbar is too full, zones try a compact style
  before shrinking. A notice offers **Use compact style** or **Show zone**.
- Icons scale in proportion on taskbars shorter than 48 DIPs, and in the
  compact style no icon is taller than its values plus 1 px.

### Labs
- New **Labs** switch at the top of the About page. It holds features that
  work but are not polished: the swell under the pointer, the zones by the
  system icons and the clock, and a few advanced position settings.
- Turning Labs off hides these and keeps their settings for later.

### Settings window
- **Quick filter** to find a setting by name.
- **Ping** has its own page.
- **Motion feel** choice (with a Custom option that shows the individual
  motion settings).
- **Preview of warning colors** on the Look page, next to the alert style.
- Hints under text boxes whose value has a problem.
- Clearer titles and descriptions written for each setting.
- About page reordered, with the log folded by default.
- Better keyboard navigation and focus.
- Fewer options shown at once: rarely used ones were pruned or folded.

### Readings editor
- Drag-and-drop shows where a reading will land: **beside**, **joined**, or
  **stacked**, with a sticky zone header while scrolling.
- **Alt+arrow keys** move the selected reading.
- The options panel shows the reading's own options first (Format, Label and
  icon, Behavior, Place), with Group style folded.
- Removed the pin button from the zone row.

### Details panel
- Lighter details panel; the Privacy button was removed from it (Privacy
  Mode is still in the settings window).

### Fixes
- `Settings page failed: 800F1000` when reopening the Presets popup.
- Double redraws while changing settings that other settings depend on.
- Memory held by closed settings pages (event handler reference cycles).
- Old daily and monthly data usage entries are pruned from storage.

## [1.0.0] - 2026-11

- First release, based on Taskbar System Info by Yevhenii Starychenko.
  Windhawk mods PR #7537.
