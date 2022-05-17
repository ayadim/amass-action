This gau Action makes it easy to orchestrate amass with GitHub Action. Integrate gau into powerful continuous security workflows and make it part of your secure software development life cycle.

Available Inputs
------

| Key               | Description                                         | Required |
| ----------------- | --------------------------------------------------- | -------- |
| `domain`          | Domain to enumerate.                                | true     |
| `config `         | Path to the INI configuration file.                 | false    |
| `brute`           | Execute brute forcing after searches.               | false    |
| `src`             | Print data sources for the discovered names.        | false    |
| `ipv4`            | Show the IPv4 addresses for discovered names.       | false    |
| `alts`            | Enable generation of altered names.                 | false    |
| `silent`          | Disable all output during execution.                | false    |
| `output`          | File to save output result (default-amass-log.txt). | false    |


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
          domain: target.com
          brute: true
          ipv4: true
          alts: true

      - name: GitHub Workflow artifacts
        uses: actions/upload-artifact@v2
        with:
          name: result
          path: amass.log



```



