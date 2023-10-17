# i18n check JSON files (against en)

A task to validate JSON locales against the `en` set of files.
The check verifies that for every `.json` file present in the `en` dir:

- the same file is present in all other locales
- all the `en` keys inside the file are also present in all the other locales

The output of the checks are listed in the task log during execution.

## Example
```console
     ...
.
├── en
│   ├── f1.json
│   ├── f2.json
│   └── f3.json     { "k1": "good morning", "k2": "good afternoon", "k3": "good evening" }
├── cy
│   ├── f1.json
│   └── f3.json     { "k1": "bore da", "k2": "prynhawn Da", "k3": "noswaith dda" }
└── de
    ├── f1.json
    ├── f2.json
    └── f3.json     { "k1": "Guten Morgen", "k2": "Guten Tag" }

```

The check of the above example will list 2 errors:

- the file `f2.json` is missing for `cy`
- in file `de`/`f3.json` the key `k3` is missing

## Inputs

| Name            | Description                                        |
| --------------- | -------------------------------------------------- |
| source-code | A directory containing the source code where the locales are also stored|


## Parameters

| Name                  | Description                   | Example              | Default   |
| --------------------- | ----------------------------- | ---------------------| ----------|
| LOCALES_DIR            | The path to the locales      | templates/languages  | locales   |

## Example
```YAML
- task: check-locales
  file: concourse-resources/tasks/i18n/json/compare-with-en/task.yml
  params:
    LOCALES_DIR: templates/languages
```
