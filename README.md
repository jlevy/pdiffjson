# pjson and pdiffjson

- **Just the simplest and fastest way to format, display, and diff JSON directly from the
  command line.** Not a fancy web UI or a library.
- [`pjson`](pjson) and [`pdiffjson`](pdiffjson) are simple bash scripts that are useful (and non-obvious) enough more
  developers should have them at their fingertips.
  They combine `jq`, `diff`, `colordiff`, and `less` to normalize, display, and diff JSON. Once you have them
  handy, you may find yourself using them a lot.
- `pjson` normalizes, colorizes, and displays one file or stdin.
- `pdiffjson` normalizes and displays a colorizied diff of any two files.
- Display and diff both ignore all non-semantic differences in formatting and whitespace.
  Only significant differences are shown in the diff output.
- The ordering of keys on collections objects is always ignored (as it should be!)
  by sorting keys.
  There’s an option to sort arrays, too, to allow unordered comparison of lists.
- Works on large files other tools barf on, thanks to `jq`’s speed.
- Diff shows context around each change, thanks to `diff`.
- Scrollable and searchable output (use space, `/`), thanks to `less`.
- Installs quickly anywhere, thanks to `npm`.
- *The feature list is longer than the code!*
  🤯😀

![example usage](images/example.gif)

## Installation

1. Ensure you have `jq` and `colordiff` on your system.

   Use `brew install jq colordiff` on Mac, `apt-get install jq colordiff` or equivalent on Linux.

2. Install the script anywhere you like.
   Simplest:

   ```bash
   $ npm install -g pdiffjson
   ```

   Or copy `pjson` and `pdiffjson` to `/usr/local/bin` by hand!

## Usage

```
$ pdiffjson
Usage: pdiffjson [--sort-arrays] [diff options] file1.json file2.json

Show pretty-printed, colored diff of normalized JSON. Uses less to
paginate the output. Allows a readable diff of any JSON, ignoring all
non-semantic differences of whitespace and key ordering.

Fields of each object are output with the keys in sorted order
prior to calling diff, so insignificant differences of key order
are ignored. The --sort-arrays option also enables recursive sorting
of all array values, so all differences in ordering within arrays
are ignored.

This is a "semi-structural diff", meaning it shows only structural
(semantic) changes but the diff is shown syntactically on JSON output,
which actually makes it more readable and flexible than a true
structural diff.

Works on large files since it relies only on diff and jq.

By default calls diff without arguments, yielding a unified diff. But
it can be helpful to add standard diff arguments to refine the type of
output, such as:
-c (contextual diff),
-C2 (contextual diff with two lines of context), or
-U5 (unified diff with 5 lines of context).

$
```

## Related Work

- [Many websites](https://www.google.com/search?q=json+diff) like
  [jsondiff](https://github.com/zgrossbart/jdd) offer JSON diff functionality but offer no
  command line, don’t work on large files, and are not good for sensitive data.
- [jsondiffpatch](https://github.com/benjamine/jsondiffpatch) is a powerful JavaScript library
  to do JSON diff and patch.
  Has a command line.
  Shows a pure structural diff.
  No semi-structured diff with context.
- [diff-json](https://github.com/andreyvit/json-diff) is another useful JavaScript library with
  a command-line interface.
  Rather slow on larger (multi-megabyte) files, with no incremental output.
- [jd](https://github.com/josephburnett/jd) is a powerful Go command line tool.
  It handles diff and patching.
  It allows more flexible diffs options on arrays (set and bag).
  No colored output or diff output options to show more context, as with diff, so the output
  seems less clear to read.
