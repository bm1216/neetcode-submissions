# Review notes — valid-sudoku (submissions 3–4)

**Verdict:** correct, accepted. Three-scan structure with [9]int count
arrays. Sub-4 exists only to remove a shipped fmt.Println — self-caught
this time, which is the ritual starting to work.

## Credits

- Bounded-domain pattern fired unprompted ([9]int, three times) one problem
  after the maps miss. Learned → automatic.
- Digit indexing via board[i][j]-'0' clean throughout.

## Improvements (his own takeaways, applied back)

1. Count-then-scan → check-before-insert (takeaway 2). A duplicate is
   detectable the moment it appears: if count already positive, return
   false. Deletes the scan loops, exits at first crime.
2. The box walk (single loop, wrapping startColumn, manual carriage
   return) needs a trace to trust. Nested loops stepping by 3 need none
   (takeaway 3).
3. Do-over target: single pass over the board updating rows/cols/boxes
   together. Key identity to DERIVE, not memorise: box = (i/3)*3 + j/3.

## Optional flourish

[9]int arrays only answer seen/not-seen. Nine bits in one int does the
same. His own Apple Notes bitwise note covers the needed ops. Trading-firm
interviewers enjoy the bitmask version.
