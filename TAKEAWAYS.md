# Rolling takeaways

Consolidated from per-problem NOTES.md. Grows as the list progresses;
re-read before the block do-over and before any timed session.

## Patterns (transferable)

1. **Bounded domain beats hashing** — 3 appearances already: `[26]int`
   counts (is-anagram), `[26]int` as map key (anagram-groups), frequency
   buckets sized `len(nums)+1` (top-k). When keys are small dense bounded
   ints, an indexed slice replaces map + sort.
2. **Check-before-insert** (two-sum one-pass): process order can make bad
   states unrepresentable — self-pair impossible, ordering free. When code
   needs guards against cases the data flow could exclude, look for the
   shape that excludes them.
3. **Simplify control flow → latent bugs die** (top-k sub-2→3): the
   readable version and the correct version were the same edit.
4. **Derive the bound, then pick the container** (top-k sub-4): frequency
   ≤ len(nums) is what justifies buckets. Say the derivation out loud in
   interviews.

5. **Prefix/suffix precomputation** (product-except-self): when answer[i]
   combines "everything left of i" and "everything right of i", build both
   with running passes. Neighbours differ by one operation. The division
   solution needed a zero case tree. This shape needed none.

## Go semantics

5. **Comma-ok vs direct indexing**: `if m[k]` only when the zero value can
   never be legitimate data (bool sets). Indices/counts: comma-ok, always
   — 0 is real data.
6. **Set idiom**: `map[T]struct{}` (zero bytes, states intent).
7. **Comparability**: arrays & all-comparable-field structs hash contents;
   pointers hash identity (mutating pointee is safe, equal contents ≠ same
   key); slices/maps/funcs never — a slice field poisons a struct key.
8. **var vs make**: nil slices fully work (append/len/range) → `var`;
   nil maps read but PANIC on write → `make`. Cap arg only when cap > len.
9. **bytes vs runes**: `s[i]` byte, `range s` rune. Byte-indexing is right
   only under an ASCII constraint — state the constraint when leaning on it.
10. **Perf lever = allocations in hot loops, not function calls** (calls
    are ns and inline; a map alloc per pair was the real cost).

## Process

11. **Pre-flight ritual**: constraint comments + "what breaks this?" before
    running. Attempt-1 failures (edge cases) stopped once this started.
12. **Failed attempts are the signature** — record what attempt 1 died of.
13. Write locally with gofmt-on-save; paste to judge. Delete dead code
    before submitting.
