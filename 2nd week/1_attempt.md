1. THINK (Attempt Before AI)
Diagnosis of Problems Found
Issues found while inspecting it:
Row Count Issue: The file has 97 rows instead of 96 rows 
Duplicate Row: Row 96 is an exact duplicate of Row 8 
Mislabeled Item: Row 40 shows `oil b` (lowercase) for City 1 on 2026-02-05 with price `108.5`. But `Oil B` already exists for that date at `318.0`. The price `108.5` actually belongs to `Staple A`.
Sentinel Missing Value: Row 30 has price "9999".
Missing Value: Row 5 has a missing (NaN) price for Pulse C in City 2 on 2026-01-01.
Planned Decisions
Row 96 (Duplicate):  delete duplicate row.
Row 40 (`oil b`): Correct item name to `Staple A`.
Row 17 (`1,250`): Clean text 
Row 30 (`9999`): Replace with "NaN", then fill using City 2 price minus 6 PKR (`157.5`).
Row 5 (`NaN`): Fill using City 1 price plus 6 PKR (`206.0`).
---
2. ASK (The Cleaning Code Court)
I asked AI for cleaning code, then tested each line of code before keeping it.
---
3. CHECK (Trial of AI Code)(used Ai)
`df.drop_duplicates()` → KEEP (Removes duplicate row 96).
`df['item'].str.title()` → REJECT (Turns `oil b` into `Oil B`, hiding the fact that row 40 was actually mislabeled `Staple A`).
`df.dropna()` → REJECT (Deletes rows with missing prices instead of fixing them accurately).
---
4. REFLECT & LOG
Summary Table of Decisions
Row	Field	Raw Value	Decision	Clean Value	Reason
96	Entire Row	Duplicate	Exclude	Deleted	Extra repeated row.
40	`item`	`oil b`	Correct	`Staple A`	Wrong label; price fits Staple A pattern.
17	`price`	`1,250`	Correct	`109.0`	Text comma and typo fix (+6 PKR city spread).
30	`price`	`9999`	Correct	`157.5`	Placeholder code; replaced using city offset.
5	`price`	`NaN`	Correct	`206.0`	Missing price; filled using city offset.
