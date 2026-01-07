# Release Notes Process

## Jira Tickets

You will be assigned four Jiras. Below are the Jiras and in the suggested order to work them:

1. Create a "shell" file for the release notes
2. Create a "placeholder" file for the release notes
3. Review the known issues and bug fixes
4. Update and assemble the CNV release notes

## Release Note Shell File

A "shell" file will need to be created so that writers can start adding release notes. The process is essentially copying over the previous version's release note file and preparing it for the new version by:

* Updating the release notes file name and anchor IDs
* Removing all content under *New and changed features* but making sure to leave headers
* Removing *Bug fixes* content
* Removing *Removed features* content

This is a step by step process with commands included. Be sure to replace `4.17` and `4.18` with the versions you are working with.

**Step 1. Check out the branch of the new version**

```bash
git checkout enterprise-4.18
git fetch upstream
```

**Step 2. Create a feature branch off of the enterprise branch**

```bash
git checkout -b CNV-XXXX
```

**Step 3. Rename the old version filename to the new version filename**

```bash
git mv virt/release_notes/virt-4-17-release-notes.adoc virt/release_notes/virt-4-18-release-notes.adoc
```

**Step 4. Replace all old version strings with the new version strings in the release notes file**

```bash
sed -i 's/virt-4-17/virt-4-18/g' virt/release_notes/virt-4-18-release-notes.adoc
```

**Step 5. Replace the old version string with the new version string in the `_topic_map.yml` file**

```bash
sed -i 's/virt-4-17-release-notes/virt-4-18-release-notes/g' _topic_maps/_topic_map.yml
```

**Step 6. Replace the old version string with the new version string in the OCP `addtl-release-notes.adoc` file**

```bash
sed -i 's/virt-4-17-release-notes/virt-4-18-release-notes/g' release_notes/addtl-release-notes.adoc
```

**Step 7. Remove section content from the release notes file**

Remove all content under **New and changed features**, **Bug fixes**, and **Removed features**, while making sure to leave the section headers in place.

**Step 8. Review Technology Preview features**

Check whether any Technology Preview features have changed status (for example, moving from Technology Preview to General Availability). If there has been a change, update the notes accordingly. If not, leave the release note as is.

**Step 9. Review Deprecated and removed features**

Check whether any deprecated features have been removed. If there has been a change, update the notes accordingly. If not, leave the release note as is.

**Step 10. Submit the pull request**

Save all changes and submit your pull request. Only merge review from the CNV team is necessary.

**Example PR**: [Link](https://github.com/openshift/openshift-docs/pull/79779)

## Release Note Placeholder File

For builds and tests to be successful in your GitHub pull request, you must open a separate PR to add a placeholder release notes file to the main branch. This is a step by step process with commands included. Be sure to replace `4.18` with the version you are working on.

**Step 1. Check out the branch of the new version**

```bash
git checkout main
git fetch upstream
```

**Step 2. Create a feature branch off of the main branch**

```bash
git checkout -b CNV-XXXX
```

**Step 3. Create a new placeholder file with the new version name**

```bash
touch virt/release_notes/virt-4-18-release-notes.adoc
```

**Step 4. Place the contents below into that file and save it**

```text
:_mod-docs-content-type: ASSEMBLY
[id="virt-4-18-release-notes"]
= {VirtProductName} release notes
include::_attributes/common-attributes.adoc[]
:context: virt-4-18-release-notes

toc::[]

Do not add or edit release notes here. Edit release notes directly in the branch
that they are relevant for.

This file is here to allow builds to work.
```

**Step 5. Save all changes and submit your pull request**

Only merge review from the CNV team is necessary.

**Example PR**: [Link](https://github.com/openshift/openshift-docs/pull/79783)

## Resources
* [OpenShift Virtualization Release Note Process Google Doc](https://docs.google.com/document/d/1nXMbam5rbReArayNSHOzzlHBK5Pi0ezCn6vXmrdOoSY/edit?usp=sharing)
