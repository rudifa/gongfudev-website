# Migration scripts

Scripts to migrate past sessions reports from [GitHub Issues](https://github.com/gongfudev/website/issues) to an Astro content collection.

## Website

The `sessions` page displays a sampling of session cards that reproduce the content of the corresponding [session](https://github.com/gongfudev/sessions) issues.

## Updating the website

This project has two node scripts used for the development of the website and updating from [session](https://github.com/gongfudev/sessions) data.

1. fetch data and save locally:

```
% scripts/fetch-repo-issues.js -s
```

2. convert the most recent 20 sessions data to astro .md files:

```
% scripts/convert-to-md.js -n 20
```

Each script has a few options helpful in the development and testing work.

```
% scripts/fetch-repo-issues.js -h

This script fetches issues from the specified github repo and saves them to a f
ile or prints them to stdout, in JSON format.

Options:
      --version    Show version number                                 [boolean]
  -c, --commented  Fetch only commented issues                         [boolean]
  -i, --invert     Invert the order of issues                          [boolean]
  -l, --log-rate   Log rate limit data from GitHub API                 [boolean]
  -r, --repo       Specify the repo               [string] [default: "sessions"]
  -o, --owner      Specify the repo owner        [string] [default: "gongfudev"]
  -s, --save       Save the fetched issues to src/data/issues.json     [boolean]
  -h, --help       Show help                                           [boolean]
```

| src/pages/                 | url                                          | Effect                                           | Status |
| :------------------------- | :------------------------------------------- | :----------------------------------------------- | ------ |
| tracks/[track].astro       | <http://localhost:4321/tracks>               | display all <tracks> tags found in sessions      | works  |
| tracks/index.astro         | <http://localhost:4321/tracks/><track>       | display links to sessions tagged with <track>    | works  |
| technos/[techno].astro     | <http://localhost:4321/technos>              | display all <technos> tags found in sessions     | works  |
| technos/index.astro        | <http://localhost:4321/technos/><techno>     | display links to sessions tagged with <techno>   | works  |
| audiences/[audience].astro | <http://localhost:4321/audiences>            | display all <audiences> tags found in sessions   | works  |
| audiences/index.astro      | <http://localhost:4321/audiences/><audience> | display links to sessions tagged with <audience> | works  |

## Generating test \*.md files

`scripts/convert-to-md.js -n 22` gives the same tags to each session, as defined in `scripts/utils/prototype.md` file.

`scripts/convert-to-md.js -n 22 -randomize` gives random tags to each session, with values defined in `scripts/utils/convert-utils.js` file.

`scripts/convert-to-md.js -i 7 -n 5` converts 5 issues starting from the 7th issue (0 based).

```
% scripts/convert-to-md.js -h

This script converts GitHub issues to markdown files.

Options:
      --version    Show version number                                 [boolean]
  -i, --index      Convert starting with ith issue         [number] [default: 0]
  -n, --number     Convert n issues             [number] [required] [default: 0]
  -r, --randomize  Randomize tags in generated files                   [boolean]
  -v, --verbose    Run with verbose logging                            [boolean]
  -h, --help       Show help                                           [boolean]
```

## Testing the current (tracks, technos, audiences) features

1. Page Sessions now displays **lists of all tags** found in all sessions, grouped under the corresponding tag type name.

2. Clicking on a tag name displays a **list of all session titles** tagged with this tag.

3. Clicking on a session title displays the session content.

4. You can open the pages for tracks, technos, and audiences by invoking the corresponding URLs (`http://localhost:4321/tracks`, `http://localhost:4321/technos`, `http://localhost:4321/audiences`).

## Branch dev-rudifa: features under development

- Propagate olange's changes on `tracks` to `technos` and `audiences`.
