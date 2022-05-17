This gau Action makes it easy to orchestrate amass with GitHub Action. Integrate gau into powerful continuous security workflows and make it part of your secure software development life cycle.



**Example**

**Workflow** - `.github/workflows/amass.yml`

**include Subdomains**
```yaml

name: 💥 amass - Amass Enum
#https://github.com/ayadim/amass-action
on:
    schedule:
      - cron: '0 0 * * *'
    workflow_dispatch:

jobs:
  amass-scan:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-go@v3
        with:
          go-version: 1.17

      - name: 💥 amass - assets Enum
        uses: ayadim/amass-action@main
        with:
          urls: input-data/gau-domains.txt
          threads: 10

      - name: GitHub Workflow artifacts
        uses: actions/upload-artifact@v2
        with:
          name: amass.log
          path: amass.log



```

**include Subdomains**

```yaml 

name: 💥 gau - archive crawler
#https://github.com/ayadim/gau-action
on:
    schedule:
      - cron: '0 0 * * *'
    workflow_dispatch:

jobs:
  gau-scan:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-go@v3
        with:
          go-version: 1.17

      - name: 💥 gau - archive crawler
        uses: ayadim/gau-action@main
        with:
          urls: input-data/gau-domains.txt
          threads: 10
          subdomains: true

      - name: GitHub Workflow artifacts
        uses: actions/upload-artifact@v2
        with:
          name: gau.log
          path: gau.log



```

Available Inputs
------

| Key               | Description                                         | Required |
| ----------------- | --------------------------------------------------- | -------- |
| `urls`            | List of urls to run nuclei scan                     | true     |
| `threads	`       | Custom templates directory/file to run nuclei scan  | false    |
| `subdomains`      | include subdomains of target domain                 | false    |
| `output`          | File to save output result (default - nuclei.log)   | false    |
| `blacklist`       | list of extensions to skip : 'jpg,txt'              | false    |
