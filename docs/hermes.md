# Hermes runtime

The dedicated Hermes profile is named `apex` and is intentionally separate from
the default profile.

## Current runtime

- Profile: `apex`
- Launcher: `~/.local/bin/apex`
- Profile home: `~/.hermes/profiles/apex/`
- Working repository: `/home/morten/code/apex`
- Native role skill: `skills/apex/SKILL.md`

Start it with:

```bash
cd /home/morten/code/apex
apex
```

If the launcher is not on `PATH`, use:

```bash
/home/morten/.local/bin/apex
```

## Recreate the profile

Profile creation is local runtime state and is not stored in Git. Recreate it
on a replacement host with Hermes installed:

```bash
hermes profile create apex --description 'Local infrastructure and development-operations agent for apex.lan. Inspect first, require approval for changes, persist durable operational context to the Apex Git repository, and verify every approved operation.' --no-alias
hermes profile use apex
hermes profile alias apex --name apex
```

Then install or copy the native skill from this repository into the new
profile's skill directory and configure the model/provider through `hermes
setup`. Never put provider keys in this repository.

## Session convention

Use the `apex` launcher, not the default `hermes` launcher, for Apex work. Start
requests with the operational goal; the profile's Apex skill supplies the role,
approval, inspection, Git persistence, and verification rules.

## Source of truth

The role and its operational records are versioned in this repository. The
profile-local skill is a runtime installation and must be synchronized from
`skills/apex/SKILL.md` after approved changes.
