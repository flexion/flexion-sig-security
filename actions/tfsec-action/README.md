# TFSEC Action

This github action scans a repository usuing AquaSecurity's [TFSEC](https://github.com/aquasecurity/tfsec) tool.

The action itself simply runs the *tfsec:latest* docker container.

## Sample Usage Yaml


```
---

on:
  pull_request:
name: Audits
jobs: 
  tfsec:
    name: tfsec audit
    runs-on: self-hosted

    steps:
      - name: Clone repo
        uses: actions/checkout@v2

      - name: tfsec
        uses: flexion/flexion-sig-security/actions/tfsec-action@master
        with:
          working_directory: ./terraform

```

## Parameters

| Key  | Value Description | Default Value |
| ---- | ----------------- | ------------- |
| `working_directory` | Directory to scan for terraform files | '.' (current directory root) |