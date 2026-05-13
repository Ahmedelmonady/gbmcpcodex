# toggle_program_activation

Enables or disables the overall Gameball loyalty program (`GbEnabled`).

## Parameter

`isActive` — `true` to enable, `false` to disable.

## Effects when disabled

- The widget **stops showing** on the storefront.
- Events from the storefront **stop being processed**.
- Existing data and integrations are **unaffected** (still readable, still stored).

## Read-before-write

Call `get_program_activation` first. State the current status to the user before toggling.

## Confirm twice for deactivation

Disabling the program is high-impact:

- At the summary: "I'll **disable** the loyalty program — widget will stop showing and events will stop processing. Are you sure?"
- Just before the call: "Final confirmation — proceed?"

Activating is low-risk; one confirmation is enough.
