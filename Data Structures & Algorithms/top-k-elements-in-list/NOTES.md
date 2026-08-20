# Review notes — top-k-elements-in-list (submission-2) — HINTS ONLY

Hints-only by request; full review after next iteration.

**Credit:** constraint comments at the top (the pre-flight ritual, now habit);
the counts→inversion insight is the heart of the optimal answer.

## Hints

1. Hand-trace the inner collection loop with nums=[1,1,2,2], k=1. How many
   elements land in output? Tests guarantee unique answers so this never
   fires here — but the tie-at-cutoff question is coming in an interview.
   One condition fixes it.
2. `for k := range values` shadows the parameter k. Harmless here — the
   dangerous kind. Rename. (Drill F12 preview.)
3. The m/index double countdown computing k-index to move forward: find the
   single readable condition that says "collection done" (something already
   knows its own length) and both counters vanish.
4. THE hint: what is the maximum value a frequency can take, given
   len(nums)? When keys are small dense ints with a known bound, what
   container indexes by them directly — no hash, no sort? The buckets are
   already built; they're in the wrong container. The sort import should
   delete itself.
5. Idiom, for later: sort.Sort(sort.Reverse(sort.IntSlice(x))) →
   sort.Ints / slices.Sort + walk backwards.
