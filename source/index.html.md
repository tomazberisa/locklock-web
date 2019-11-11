---
title: locklock documentation

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - python

toc_footers:
  - <a href='mailto:support@locklock.io'>Support</a>
  - <a href='https://docs.locklock.io'>Link to this page</a>

# includes:
#   - errors

# search: true
---

# Introduction

Welcome to the Locklock documentation!

Locklock is a REST API for simple distributed locking. Acquiring a lock is as easy as `POST`ing to an endpoint and releasing that same lock is done by `DELETE`ing that same endpoint.

When accessed by multiple clients at the same time, locklock guarantees only one of the incoming requests will acquire the specified lock.

Locklock was designed to be instantly usable and is accessible as a free public service at `https://public.locklock.io/v1/api`.

# Quickstart

```shell
curl -X POST \
    -H "Content-Type: application/json" \
    https://public.locklock.io/v1/api/lock/uuid/180da65c-cf80-4997-8574-0c0801817d6f
```

Acquiring a lock is as simple as:

`POST https://public.locklock.io/v1/api/lock/uuid/<uuid>`

```shell
curl -X DELETE \
    -H "Content-Type: application/json" \
    https://public.locklock.io/v1/api/lock/uuid/180da65c-cf80-4997-8574-0c0801817d6f
```

Releasing an acquired lock is accomplished by:

`DELETE https://public.locklock.io/v1/api/lock/uuid/<uuid>`

# Usage

```shell
curl -X POST \
    -d '{"secret":"super-secret", "expires_in": 300}' \
    -H "Content-Type: application/json" \
    https://public.locklock.io/v1/api/lock/uuid/180da65c-cf80-4997-8574-0c0801817d6f
```

The user may specify two POST parameters:

- `expires_in`: specifies the lock expiration time in seconds (default: 30 days)
- `secret`: specifies a secret that is required to release the lock

```shell
curl -X DELETE \
    -d '{"secret":"super-secret"}' \
    -H "Content-Type: application/json" \
    https://public.locklock.io/v1/api/lock/uuid/180da65c-cf80-4997-8574-0c0801817d6f
```

If a `secret` is provided when acquiring the lock, a `secret` is required to release the lock (unless the lock expires).

# Pro accounts

For users with production-level requirements, paid Pro accounts are available. Please contact <a href='mailto:support@locklock.io'>support@locklock.io</a> for more information.

Feature | Developer | Pro
--------- | ----------- | -----------
Access to public API | + | +
UUID-named locks (`/lock/uuid/<uuid>`) | + | +
Custom subdomain | - | +
Custom (non-UUID) lock names (`/lock/key/<custom-name>`) | - | +
API key | - | +
Higher throttling limits | - | +
Custom AWS regions | - | +
Enhanced support | - | +
