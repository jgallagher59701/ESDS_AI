# Work Log

## 2026-06-01 16:06 MDT

Query/prompt: "Update the table in the `Budget Summary` section with new values from @Budget.csv. Edit the filr @main.tex."

- Read `Budget.csv` and compared its values to the existing `Budget Summary` table in `main.tex`.
- Updated Hannah Robertson's months and cost to match the CSV.
- Updated the `Tooling` row to use `n/a` values from the CSV.
- Updated the table total to `$186,785`.

## 2026-05-31 09:57 MDT

Query/prompt: "Read @Budget.csv and insert that data as a table in the `Budget Summary` section. Edit the main.tex file. Do not add any additional text."

- Located the `Budget Summary` section in `main.tex`.
- Read `Budget.csv` and extracted the tabular data.
- Inserted a LaTeX `tabular` environment into the `Budget Summary` section without adding prose outside the table.
- Kept the existing section text unchanged.
