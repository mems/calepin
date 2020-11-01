> CSV files are a little bit like like dates: superficially simple, with lots of corner cases. Largely for the same reason: not in accordance with standard.

- [RFC 4180 - Common Format and MIME Type for Comma-Separated Values (CSV) Files](https://tools.ietf.org/html/rfc4180)
- [CSV.js/csv.js at master · knrz/CSV.js](https://github.com/knrz/CSV.js/blob/master/csv.js)
- [CSV Project - Node.js CSV package](https://csv.js.org/)
- awk
	- [Awk-Batteries/Units/csv at master · Nomarian/Awk-Batteries](https://github.com/Nomarian/Awk-Batteries/tree/master/Units/csv)
	- [Awk-Batteries/csv.awk at master · Nomarian/Awk-Batteries](https://github.com/Nomarian/Awk-Batteries/blob/master/Units/csv.awk) - parse CSV `gawk -f "$AWK/Units/csv.awk" -e '{print NF}'`
	- [What's the most robust way to efficiently parse CSV using awk? - Stack Overflow](https://stackoverflow.com/questions/45420535/whats-the-most-robust-way-to-efficiently-parse-csv-using-awk)
- [How to convert arbitrary simple JSON to CSV using jq? - Stack Overflow](https://stackoverflow.com/questions/32960857/how-to-convert-arbitrary-simple-json-to-csv-using-jq)
- `sqlite3 cities.db ".mode csv" ".import ./city.csv cities" ".exit"` [Command Line Shell For SQLite](https://sqlite.org/cli.html)
- [johnkerl/miller: Miller is like awk, sed, cut, join, and sort for name-indexed data such as CSV, TSV, and tabular JSON](https://github.com/johnkerl/miller)
- [BurntSushi/xsv: A fast CSV command line toolkit written in Rust.](https://github.com/BurntSushi/xsv)
- [harelba/q: q - Run SQL directly on CSV or TSV files](https://github.com/harelba/q)
- [wireservice/csvkit: A suite of utilities for converting to and working with CSV, the king of tabular file formats.](https://github.com/wireservice/csvkit)

## Alternative formats

- [Tab-separated values - Wikipedia](https://en.wikipedia.org/wiki/Tab-separated_values)
- [Text File formats – ASCII Delimited Text – Not CSV or TAB delimited text | Ronald Duncan's Blog](https://web.archive.org/web/20201028172315/https://ronaldduncan.wordpress.com/2009/10/31/text-file-formats-ascii-delimited-text-not-csv-or-tab-delimited-text/)
