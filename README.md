# dbeaver-drivers

DBeaver's Maven driver cache, lifted verbatim from a machine that can reach
Maven Central, for one that cannot. DBeaver downloads JDBC drivers on first
connect; on a network that blocks that download it simply fails to connect.
Pre-seeding the cache from this repo makes the download a cache hit.

Contents: the **PostgreSQL** driver set (`postgresql` 42.7.2 and 42.7.11,
PostGIS 2.5.0) and their transitive dependencies (jna, waffle, caffeine,
byte-buddy, slf4j, checker-qual, error-prone). 39 files, ~16 MB. Nothing else.

## Install

Clone, then copy `maven-central/` into DBeaver's cache, preserving layout:

```powershell
robocopy "$PWD\maven-central" "$env:APPDATA\DBeaverData\drivers\maven\maven-central" /E
```

Restart DBeaver. The PostgreSQL driver should show as downloaded without a
network request. If DBeaver still tries to download, check the driver's
version in *Database → Driver Manager → PostgreSQL → Libraries* matches one
of the versions here (42.7.11 is current).

## Verify after clone

```powershell
sha256sum -c MANIFEST.sha256
```

(from Git Bash; every line should say `OK`). The manifest was generated from
the original files, so a clone that alters anything will show it.

## Licensing

Private repo, for personal transfer only. The artifacts carry their own
licences (PostgreSQL JDBC: BSD-2; others: Apache-2.0 / MIT / LGPL) and are
unmodified copies of what Maven Central serves.
