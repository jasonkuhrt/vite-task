# fetch_env_explicit_read_overrides_untracked_config

An explicit tracked getEnv call remains a dependency even when the task declares the same name in untrackedEnv.

## `PROBE_ENV=first vt run fetch-env-explicitly-untracked`

populate: getEnv explicitly records the otherwise untracked value

```
$ node scripts/fetch_env.mjs PROBE_ENV
served PROBE_ENV=first
process.env PROBE_ENV=first
```

## `PROBE_ENV=first vt run fetch-env-explicitly-untracked`

cache hit: the explicit dependency is unchanged

```
$ node scripts/fetch_env.mjs PROBE_ENV ◉ cache hit, replaying
served PROBE_ENV=first
process.env PROBE_ENV=first

---
vt run: cache hit.
```

## `PROBE_ENV=second vt run fetch-env-explicitly-untracked`

cache miss: an explicit getEnv read stays tracked

```
$ node scripts/fetch_env.mjs PROBE_ENV ○ cache miss: env 'PROBE_ENV' changed, executing
served PROBE_ENV=second
process.env PROBE_ENV=second
```
