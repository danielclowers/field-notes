# Content Quality Assessment

## Process

<!-- WIP -->

## Helpful Commands

Run Vale on an assembly and all modules included in it:

```
vale --minAlertLevel=warning example-assembly.adoc $(grep -oP 'include::\K[^[]+' example-assembly.adoc | grep -v '_attributes/common-attributes.adoc')
```

List `_mod-docs-content-type` for all modules included in an assembly and print `MISSING` if the attribute is not present:

```
for f in $(grep -oP 'include::\K[^[]+' example-assembly.adoc | grep '^modules/' | sort -u); do echo "==> $f <=="; grep '^:_mod-docs-content-type:' "$f" || echo 'MISSING'; echo; done
```

## Resources

<!-- WIP -->
