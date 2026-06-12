# Copy & Microcopy Bank

> Approved wording for every recurring UI moment. When in doubt, lift directly from here. Keep voice: direct, calm, no exclamation points unless celebrating a Peak-End completion.

## Voice Principles

1. **Active, not passive.** "Sync failed" not "A sync error has occurred."
2. **Subject + verb.** Don't be cute. "Saving..." not "Hold tight, we're working on it!"
3. **No marketing fluff.** "Connect" not "Let's get you connected!"
4. **One sentence.** If it needs two, it's the wrong moment for that copy.
5. **Sentence case for labels.** Title Case only for proper names and tab headers.
6. **No emojis** in functional UI. Reserved for casual surfaces explicitly approved by Antonio.
7. **No exclamation points** except for genuine Peak-End completion moments.

---

## Button Labels (Primary CTAs)

### Action verbs (preferred)
- `Run sweep` — start an automated process
- `Sync now` — manual trigger of background sync
- `Export` — produce a file from current state
- `Save changes` — persist edits (only when ambiguous; otherwise just `Save`)
- `Save` — persist new or edited record
- `Continue` — proceed in a multi-step flow
- `Connect` — establish a link to a service or device
- `Reconnect` — restore a lost connection
- `Generate` — kick off an AI or compute task
- `Apply` — commit a setting change without closing the panel
- `Confirm` — explicit acknowledgement before a destructive or expensive action

### Destructive actions
- `Delete` — soft delete (recoverable)
- `Delete permanently` — hard delete (irreversible)
- `Discard changes` — abandon unsaved edits
- `Disconnect` — unlink without deleting
- `Cancel sweep` — abort a running process
- `Revert` — return to last saved state

### Forbidden
- `Submit` — too generic, name the outcome
- `OK` — meaningless in a button context
- `Click here` — never
- `Yes` / `No` standalone — name the action both buttons commit to

---

## Snackbar Messages (Peak-End Completion)

Format: `<Subject> <verb past-tense>.` Optional second clause for context. Max 60 characters.

### Success
- `Sweep complete. 47 entries logged.`
- `Synced. 3 recipes added to Thermomix.`
- `Saved.`
- `Export ready. File downloaded.`
- `Connected to <node-name>.`
- `Settings applied.`

### In-progress (rare — prefer skeleton screens)
- `Syncing...`
- `Generating preview...`
- `Exporting...`

### Soft confirmations
- `Copied to clipboard.`
- `Link copied.`
- `Draft saved.`

---

## Error Messages

Format: `<What failed>. <What to try.>` Two sentences. Never expose error codes in the body — surface them in a "Details" link.

### Connection errors
- `Can't reach <node-name>. Check the network connection and try again.`
- `Sync failed. The Thermomix didn't respond — verify it's powered on.`
- `Connection lost. Reconnecting automatically.`

### Validation errors (inline below the field)
- `Required.`
- `Use a valid email.`
- `Must be 8 characters or longer.`
- `That username is taken.`

### Permission errors
- `You don't have access to this resource.`
- `Sign in to continue.`

### Generic fallback (use sparingly)
- `Something went wrong. Try again in a moment.`

### Forbidden
- Raw tracebacks
- "An error occurred"
- "Oops!"
- "Uh oh"
- Stack frame references

---

## Empty State Copy

Format: `<One-line description of the empty state>` + primary CTA below.

### Examples
- **No sweep history yet** — `Run initial sweep`
- **No recipes synced** — `Sync from Thermomix`
- **No connected nodes** — `Add a node`
- **No saved searches** — `Save your first search`
- **No drafts** — `Start writing`
- **Inbox zero** — `You're caught up.` (no CTA — celebrate the moment)

### Forbidden
- `No data available`
- `Nothing here`
- `No items found` (acceptable for search results — see below)

---

## Loading State Copy

Prefer **skeleton screens** with no text. When text is required:

- `Loading...` — last resort, always show a skeleton with it
- `Almost ready...` — only after 5+ seconds
- `This is taking longer than usual. Hang on.` — only after 15+ seconds

---

## Search Results

- `0 results for "<query>"` — followed by suggestions: `Try a broader term.`
- `<n> results` — for any count > 0
- `Showing <n> of <total>` — when results are paginated/truncated

---

## Confirmation Dialogs (Destructive Actions Only)

Use only when the action is irreversible AND consequential. Otherwise, ship it and offer Undo.

Format:
- **Title:** Question form. `Delete this sweep?`
- **Body:** State the consequence. `This will remove 47 log entries. This cannot be undone.`
- **Buttons:** Verb-named. `Delete sweep` (destructive style) + `Cancel`.

### Examples
- `Discard unsaved changes? You've made 3 edits that haven't been saved.` → [Discard changes] [Keep editing]
- `Disconnect from <node-name>? Active syncs will stop immediately.` → [Disconnect] [Cancel]
- `Delete this recipe permanently? It will be removed from the Thermomix on next sync.` → [Delete permanently] [Cancel]

---

## Onboarding First-Run

Lead with what the user can do, not what the app is.

- `Connect your first node to start monitoring.`
- `Add a Thermomix to begin syncing recipes.`
- `Pick a folder to watch. We'll handle the rest.`

### Forbidden
- `Welcome to <AppName>!` (they know — they opened it)
- "Let's get you set up" (just do it)
- Multi-page tutorials before any value is shown

---

## Form Labels

- Above the input, not inside.
- Sentence case.
- No colons.
- No "Please" or "Enter your" — just name the field.

| Don't | Do |
|---|---|
| `Please enter your email:` | `Email` |
| `Choose a password (required)` | `Password` |
| `What's your name?` | `Name` |
| `Select an option` | `Status` |

---

## Tooltips (Allowed Only Where Conventions Demand)

The covenant says no tooltips for primary actions. Exceptions where tooltips are expected:

- Toolbar icon buttons in AEC plugins (host convention)
- Truncated table cells (show full value on hover)
- Keyboard shortcut hints (e.g., `Save (⌘S)`)

### Format
- Verb phrase or noun phrase. No sentences.
- `Save changes` or `Saved at 2:14 PM`
- Not `Click this button to save your changes`

---

## Accessibility Copy (Screen Readers)

### `aria-label` for icon-only buttons
- `Close dialog`
- `Open menu`
- `Sort by date, ascending`

### Live region announcements
- `<n> new notifications` — politeness `polite`
- `Connection lost. Attempting reconnect.` — politeness `assertive`

### Skip links
- `Skip to main content`
- `Skip to navigation`

---

## Localization Notes

When translating later:
- Reserve **30% extra horizontal space** for German.
- Reserve **20% extra** for French, Spanish, Italian.
- Reserve **40% less** for CJK (vertical density increases).
- Date/time always uses locale formatting, never hard-coded `MM/DD/YYYY`.
