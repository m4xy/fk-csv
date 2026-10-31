# fk-csv

CSV for fckt, as RFC 4180 describes it: rows of fields, separated by commas, a line each.

```kotlin
import uk.m4xy.csv.Csv

Csv.parse("name,said\nAda,\"\"\"hello\"\", she said\"\n")
// Ok([["name", "said"], ["Ada", "\"hello\", she said"]])

Csv.write([["id", "note"], ["1", "with, comma"]])
// id,note
// 1,"with, comma"

Csv.records("name,age\nAda,36\n")
// Ok([[("name", "Ada"), ("age", "36")]])
```

`Csv.parse` reads every row, or says what's wrong and on which line: a quoted field that isn't
closed, or something after a field's closing quote. A field in quotes can have the separator,
line breaks and doubled quotes in it; lines can end with `\n` or `\r\n`, and the last needn't end
at all. `Csv.write` puts a field in quotes only when it needs them, and `lineEnd` can be `"\r\n"`,
as RFC 4180 has it. `Csv.records` names each row's fields by the first row's, and says which row
has more or fewer than it; `Csv.field` gives a record's field by its name. Each takes another
separator, as `';'`, if it's given one.

## Building

```sh
kiln build          # compiles and tests it
kiln publishLocal   # for other projects: library("uk.m4xy:fk-csv:0.1.0")
```
