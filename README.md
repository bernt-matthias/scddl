Scientific Computing Data Set Download
======================================

**scddl** (pronounced **scuttle**) downloads data sets for scientific
computing.


Table of Contents
-----------------

<!-- toc -->

- [Goals and Features](#goals-and-features)
  * [Consistency](#consistency)
  * [Usability](#usability)
- [Supported Data Sets](#supported-data-sets)
- [Usage](#usage)

<!-- tocstop -->


Goals and Features
------------------

### Consistency

-   **integrity checks**

    Data sets that provide file integrity information, e.g. MD5 checksums, are
    rigorously checked.

-   **strict versioning**

    Data sets that are not inherently versioned will be tagged with the
    download date. This makes **reproducible research** possible. Additionally,
    these data sets have a link to the latest version.

    A result of this is that **existing files are never overwritten**. All
    running jobs would have inconsistent results if files would be updated in
    place.


### Usability

-   **centralized storage location**

    Especially on scientific computing platforms, the data sets are intended to
    be downloaded to globally accessible storage locations. This avoids that
    users or groups have to maintain their own copies and that their file
    system quotas are stressed. The system administrators can lift this burden
    off of their users.

    Another advantage of a centralized storage location is that the file system
    can better cache the data sets when multiple users access it. This can
    result in better I/O performance.

-   **automatic updates**

    The download tools are designed to be run as **cron jobs** or **systemd
    timers**. You can, of course, run them manually, but the real convenience
    benefit comes from automation.

-   **logging to syslog**

    The download tools send their output to syslog with their script name as
    the tag, e.g. the tool **ncbidl.sh** would use **ncbidl** as tag. You can
    then search for these tags, e.g.:

        journalctl -t ncbidl


Supported Data Sets
-------------------

- [NCBI](https://ftp.ncbi.nlm.nih.gov)
  - requires **lftp**


Usage
-----

Intended to be used as cron jobs, e.g.:

```
@monthly time bash /path/to/ncbidl.sh blast/db/nr /data/db
@monthly time bash /path/to/ncbidl.sh blast/db/nt /data/db
```
