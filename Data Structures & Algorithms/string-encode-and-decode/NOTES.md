# Review notes — string-encode-and-decode (submission-4) — HINTS

Accepted but breakable; his own "not proud" verdict is correct. Full review
after redesign.

## Two legal inputs that break it

- `["-100"]` → encodes to `"-100"` → decodes to `[]` (empty-array sentinel
  collides with real data)
- `["a#!~/100b"]` → Split shreds the stored string (delimiter collision)

Same disease twice: **in-band signalling**. Any marker living in the data
channel can be forged by data. A weirder delimiter lowers probability;
never reaches zero. Design problem = adversarial correctness, so "unlikely"
= wrong.

## Hint

How does an HTTP response bound a body that can contain anything?
What information, placed AHEAD of each string, answers "where does it
stop?" without inspecting contents? Note the empty array then needs no
sentinel at all.

## Hygiene

- `fmt.Println(input)` shipped in Decode — delete debug output.
- `for idx, s := range strs` shadows receiver `s` — THIRD shadowing
  sighting (param k in top-k, now this). Watch for it; F12 incoming.
- `output += s` in a loop is O(n²) rebuild — strings.Builder is the tool,
  first natural use case in the list.

## Also today

top-k submission-5: pre-sized the frequency map same day as the review
note. Feedback→habit latency of hours.
