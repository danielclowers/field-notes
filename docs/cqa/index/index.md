# Content Quality Assessment

## Process

<!-- WIP -->

## Helpful Commands

Run Vale on a specific assembly and all modules included in it:

```
vale --minAlertLevel=warning \
example-assembly.adoc \
$(grep -oP 'include::\K[^[]+' example-assembly.adoc \
  | grep -v '_attributes/common-attributes.adoc')
```

Run Vale on a directory of assemblies and all modules included in those assemblies:

```
vale --minAlertLevel=warning \
$(find virt/live_migration -name "*.adoc") \
$(grep -rhoP 'include::\K[^[]+' virt/live_migration | grep -v '_attributes/common-attributes.adoc' | sort -u)
```

List `_mod-docs-content-type` for all modules included in an assembly and print `MISSING` if the attribute is not present:

```
for f in $(grep -oP 'include::\K[^[]+' example-assembly.adoc \
  | grep '^modules/' \
  | sort -u); do
  echo "==> $f <=="
  grep '^:_mod-docs-content-type:' "$f" || echo 'MISSING'
  echo
done
```

## Resources

<!-- WIP -->
