# get_program_activation

Returns the current Gameball program activation state — client settings including whether the loyalty program (`GbEnabled`) is active or inactive.

## Notes

- Required first step before `toggle_program_activation`.
- This is a top-level kill switch — when off, the widget stops showing and storefront events stop being processed.
