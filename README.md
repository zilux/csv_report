Role Name: csv_report
=========

[![CI](https://github.com/zilux/csv_report/actions/workflows/ci.yml/badge.svg?branch=main)](https://github.com/zilux/csv_report/actions/workflows/ci.yml)


Create csv file and mail this file.
---

You can create small tests and include this in your report.

For an item in your report you need e.g. in site.yml one row
```
 - role: csv_report
   run_tasks:
     - { run: 'oom_check.yml', header: 'oom_last', outcome_in: ['oom_last_outcome'] }
```

```
run:  <test in tasks>
header: <header line of report>
outcome_in:  < var which is filled with outcome in <test in task>
```

Requirements
------------

You need a mail gateway which send your created csv file.
You also can set param must_mail to false to see only output.

Role Variables
--------------

  must_mail: true
  delegate_host: mailhub.example.com
  email_to:
    - mail_account@gmail.com


Dependencies
------------

Needed community.general

Example Playbook
----------------

```
  ---
  - name: Run check
    hosts: all
    become: true
    gather_facts: false

    tasks:

    roles:

      - role: zilux.csv_report
        run_tasks:
          - { run: 'reachable.yml', header: 'reachable', outcome_in: ['setup_ok'] }
          - { run: 'oom_check.yml', header: 'oom_last', outcome_in: ['oom_last_outcome'] }
          - { run: 'rpmdb_check.yml', header: 'rpmdb_failed', outcome_in: ['rpmdb_failed'] }
          - { run: 'check_cpu_mem_uptime.yml', header: 'uptime,cpu,mem', outcome_in: ['uptime', 'procs', 'memtot'] }
          - { run: 'get_swap.yml', header: 'mem_available,swap_total,swap_free', outcome_in: ['mem_available', 'swap_total', 'swap_free'] }
          - { run: 'status_repos.yml', header: 'repos', outcome_in: ['status_repo'] }
```

License
-------

license GPL-2.0-or-later

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
