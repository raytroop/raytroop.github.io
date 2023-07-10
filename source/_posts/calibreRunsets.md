---
title: Calibre Runsets
date: 2023-08-10 23:11:08
tags:
categories:
- cad
---



Calibre Interactive stores a list of your most recently opened runsets in your *home directory* as `.cgidrcdb` or `.cgilvsdb` for Calibre Interactive DRC or LVS, respectively. 

When invoked, the Calibre DRC and LVS windows automatically load the runset used when the last session was closed. 

> Runsets are ASCII files that set up Calibre Interactive for a Calibre run. They contain only information that differs from the default configuration of Calibre Interactive. There is a one-to-one correspondence between entry lines in the runset file and fields and button items in the Calibre Interactive user interface. Here is as example of a DRC runset:
>
> ```
> *drcRulesFile: rule_file
> *drcRulesFileLastLoad: 1009224452
> *drcLayoutPaths: ./lab3.gds
> *drcLayoutPrimary: lab3
> *drcResultsFile: ./lab3.db
> *drcSummaryFile: drc_report
> *drcRunTurbo: 0
> *drcRunRemoteOn: Cluster
> *drcRemoteLICENSEFILEName: MGLS_LICENSE_FILE
> *drcRemoteLICENSEFILEValue: /scratch1/mgls/mgclicenses
> *drcDontWaitForLicense: 0
> ```



---

The runset filename opened at startup (if no runset is specified on the command line) can also be specified by setting the `MGC_CALIBRE_DRC_RUNSET_FILE` environment variable for DRC, and the `MGC_CALIBRE_LVS_RUNSET_FILE` environment variable for LVS. If these environment variables are set, they take precedence over all other runset opening behavior options. 

```
setenv RUNSET_DIR ../calibre
setenv MGC_CALIBRE_DRC_RUNSET_FILE $RUNSET_DIR/tsmc180nm_drc_runset
setenv MGC_CALIBRE_LVS_RUNSET_FILE $RUNSET_DIR/tsmc180nm_lvs_runset
setenv MGC_CALIBRE_PEX_RUNSET_FILE $RUNSET_DIR/tsmc180nm_pex_runset
setenv CALIBRE_DISABLE_RHEL5_WARNING 1
```



## reference

tsmc_template. [https://github.com/lnis-uofu/tsmc_template/tree/main](https://github.com/lnis-uofu/tsmc_template/tree/main)

Calibre Verification User’s Manual
