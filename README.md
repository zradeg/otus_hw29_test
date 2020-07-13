Три хоста с говорящими названиями: pgmaster, pgslave, barman
Репликация между pgmaster и pgslave работает. Бэкапирование на barman не работает, застревает на этом моменте:

```
[root@barman .ssh]# barman backup pgmaster
Starting backup using postgres method for server pgmaster in /var/lib/barman/pgmaster/base/20200713T124758
Backup start at LSN: 0/5A000140 (00000001000000000000005A, 00000140)
Starting backup copy via pg_basebackup for 20200713T124758
```

```
[root@barman .ssh]# barman check pgmaster
Server pgmaster:
        PostgreSQL: OK
        superuser or standard user with backup privileges: OK
        PostgreSQL streaming: OK
        wal_level: OK
        replication slot: OK
        directories: OK
        retention policy settings: OK
        backup maximum age: OK (no last_backup_maximum_age provided)
        compression settings: OK
        failed backups: FAILED (there are 17 failed backups)
        minimum redundancy requirements: FAILED (have 0 backups, expected at least 5)
        pg_basebackup: OK
        pg_basebackup compatible: OK
        pg_basebackup supports tablespaces mapping: OK
        systemid coherence: OK
        pg_receivexlog: OK
        pg_receivexlog compatible: OK
        receive-wal running: OK
        archive_mode: OK
        archive_command: OK
        archiver errors: OK
```

```
[root@barman .ssh]# barman diagnose
{
    "global": {
        "config": {
            "backup_options": "concurrent_backup",
            "barman_home": "/var/lib/barman",
            "barman_user": "barman",
            "compression": "gzip",
            "configuration_files_directory": "/etc/barman.d",
            "errors_list": [],
            "log_file": "/var/log/barman/barman.log",
            "log_level": "INFO",
            "minimum_redundancy": "2",
            "recovery_options": "'get-wal'",
            "retention_policy": "RECOVERY WINDOW OF 2 WEEKS",
            "streaming_archiver_name": "barman_receive_wal"
        },
        "system_info": {
            "barman_ver": "2.11",
            "kernel_ver": "Linux barman 3.10.0-957.12.2.el7.x86_64 #1 SMP Tue May 14 21:24:32 UTC 2019 x86_64 x86_64 x86_64 GNU/Linux",
            "python_ver": "",
            "release": "RedHat Linux CentOS Linux release 7.8.2003 (Core)",
            "rsync_ver": "rsync  version 3.1.2  protocol version 31",
            "ssh_ver": "",
            "timestamp": "Mon Jul 13 12:48:45 2020"
        }
    },
    "servers": {
        "pgmaster": {
            "backups": {
                "20200712T040723": {
                    "backup_id": "20200712T040723",
                    "backup_label": null,
                    "begin_offset": 2776,
                    "begin_time": "Sun Jul 12 04:07:23 2020",
                    "begin_wal": "000000010000000000000025",
                    "begin_xlog": "0/25000AD8",
                    "config_file": "/var/lib/pgsql/11/data/postgresql.conf",
                    "copy_stats": null,
                    "deduplicated_size": null,
                    "end_offset": null,
                    "end_time": null,
                    "end_wal": null,
                    "end_xlog": null,
                    "error": "failure copying files (KeyboardInterrupt)",
                    "hba_file": "/var/lib/pgsql/11/data/pg_hba.conf",
                    "ident_file": "/var/lib/pgsql/11/data/pg_ident.conf",
                    "included_files": null,
                    "mode": "postgres",
                    "pgdata": "/var/lib/pgsql/11/data",
                    "server_name": "pgmaster",
                    "size": null,
                    "status": "FAILED",
                    "systemid": "6847607985520892865",
                    "tablespaces": null,
                    "timeline": 1,
                    "version": 110008,
                    "xlog_segment_size": 16777216
                },
                "20200712T164429": {
                    "backup_id": "20200712T164429",
                    "backup_label": null,
                    "begin_offset": 600,
                    "begin_time": "Sun Jul 12 16:44:29 2020",
                    "begin_wal": "000000010000000000000029",
                    "begin_xlog": "0/29000258",
                    "config_file": "/var/lib/pgsql/11/data/postgresql.conf",
                    "copy_stats": null,
                    "deduplicated_size": null,
                    "end_offset": null,
                    "end_time": null,
                    "end_wal": null,
                    "end_xlog": null,
                    "error": "failure copying files (KeyboardInterrupt)",
                    "hba_file": "/var/lib/pgsql/11/data/pg_hba.conf",
                    "ident_file": "/var/lib/pgsql/11/data/pg_ident.conf",
                    "included_files": null,
                    "mode": "postgres",
                    "pgdata": "/var/lib/pgsql/11/data",
                    "server_name": "pgmaster",
                    "size": null,
                    "status": "FAILED",
                    "systemid": "6847607985520892865",
                    "tablespaces": null,
                    "timeline": 1,
                    "version": 110008,
                    "xlog_segment_size": 16777216
                },
                "20200712T175320": {
                    "backup_id": "20200712T175320",
                    "backup_label": null,
                    "begin_offset": 96,
                    "begin_time": "Sun Jul 12 17:53:20 2020",
                    "begin_wal": "00000001000000000000002C",
                    "begin_xlog": "0/2C000060",
                    "config_file": "/var/lib/pgsql/11/data/postgresql.conf",
                    "copy_stats": null,
                    "deduplicated_size": null,
                    "end_offset": null,
                    "end_time": null,
                    "end_wal": null,
                    "end_xlog": null,
                    "error": "failure copying files (KeyboardInterrupt)",
                    "hba_file": "/var/lib/pgsql/11/data/pg_hba.conf",
                    "ident_file": "/var/lib/pgsql/11/data/pg_ident.conf",
                    "included_files": null,
                    "mode": "postgres",
                    "pgdata": "/var/lib/pgsql/11/data",
                    "server_name": "pgmaster",
                    "size": null,
                    "status": "FAILED",
                    "systemid": "6847607985520892865",
                    "tablespaces": null,
                    "timeline": 1,
                    "version": 110008,
                    "xlog_segment_size": 16777216
                },
                "20200712T180508": {
                    "backup_id": "20200712T180508",
                    "backup_label": null,
                    "begin_offset": 96,
                    "begin_time": "Sun Jul 12 18:05:08 2020",
                    "begin_wal": "000000010000000000000030",
                    "begin_xlog": "0/30000060",
                    "config_file": "/var/lib/pgsql/11/data/postgresql.conf",
                    "copy_stats": null,
                    "deduplicated_size": null,
                    "end_offset": null,
                    "end_time": null,
                    "end_wal": null,
                    "end_xlog": null,
                    "error": "failure copying files (KeyboardInterrupt)",
                    "hba_file": "/var/lib/pgsql/11/data/pg_hba.conf",
                    "ident_file": "/var/lib/pgsql/11/data/pg_ident.conf",
                    "included_files": null,
                    "mode": "postgres",
                    "pgdata": "/var/lib/pgsql/11/data",
                    "server_name": "pgmaster",
                    "size": null,
                    "status": "FAILED",
                    "systemid": "6847607985520892865",
                    "tablespaces": null,
                    "timeline": 1,
                    "version": 110008,
                    "xlog_segment_size": 16777216
                },
                "20200712T182551": {
                    "backup_id": "20200712T182551",
                    "backup_label": null,
                    "begin_offset": 96,
                    "begin_time": "Sun Jul 12 18:25:51 2020",
                    "begin_wal": "000000010000000000000033",
                    "begin_xlog": "0/33000060",
                    "config_file": "/var/lib/pgsql/11/data/postgresql.conf",
                    "copy_stats": null,
                    "deduplicated_size": null,
                    "end_offset": null,
                    "end_time": null,
                    "end_wal": null,
                    "end_xlog": null,
                    "error": "failure copying files (data transfer failure on directory '/var/lib/barman/pgmaster/base/20200712T182551/data')",
                    "hba_file": "/var/lib/pgsql/11/data/pg_hba.conf",
                    "ident_file": "/var/lib/pgsql/11/data/pg_ident.conf",
                    "included_files": null,
                    "mode": "postgres",
                    "pgdata": "/var/lib/pgsql/11/data",
                    "server_name": "pgmaster",
                    "size": null,
                    "status": "FAILED",
                    "systemid": "6847607985520892865",
                    "tablespaces": null,
                    "timeline": 1,
                    "version": 110008,
                    "xlog_segment_size": 16777216
                },
                "20200712T182636": {
                    "backup_id": "20200712T182636",
                    "backup_label": null,
                    "begin_offset": 96,
                    "begin_time": "Sun Jul 12 18:26:36 2020",
                    "begin_wal": "000000010000000000000035",
                    "begin_xlog": "0/35000060",
                    "config_file": "/var/lib/pgsql/11/data/postgresql.conf",
                    "copy_stats": null,
                    "deduplicated_size": null,
                    "end_offset": null,
                    "end_time": null,
                    "end_wal": null,
                    "end_xlog": null,
                    "error": "failure copying files (data transfer failure on directory '/var/lib/barman/pgmaster/base/20200712T182636/data')",
                    "hba_file": "/var/lib/pgsql/11/data/pg_hba.conf",
                    "ident_file": "/var/lib/pgsql/11/data/pg_ident.conf",
                    "included_files": null,
                    "mode": "postgres",
                    "pgdata": "/var/lib/pgsql/11/data",
                    "server_name": "pgmaster",
                    "size": null,
                    "status": "FAILED",
                    "systemid": "6847607985520892865",
                    "tablespaces": null,
                    "timeline": 1,
                    "version": 110008,
                    "xlog_segment_size": 16777216
                },
                "20200712T182711": {
                    "backup_id": "20200712T182711",
                    "backup_label": null,
                    "begin_offset": 264,
                    "begin_time": "Sun Jul 12 18:27:11 2020",
                    "begin_wal": "000000010000000000000036",
                    "begin_xlog": "0/36000108",
                    "config_file": "/var/lib/pgsql/11/data/postgresql.conf",
                    "copy_stats": null,
                    "deduplicated_size": null,
                    "end_offset": null,
                    "end_time": null,
                    "end_wal": null,
                    "end_xlog": null,
                    "error": "failure copying files (data transfer failure on directory '/var/lib/barman/pgmaster/base/20200712T182711/data')",
                    "hba_file": "/var/lib/pgsql/11/data/pg_hba.conf",
                    "ident_file": "/var/lib/pgsql/11/data/pg_ident.conf",
                    "included_files": null,
                    "mode": "postgres",
                    "pgdata": "/var/lib/pgsql/11/data",
                    "server_name": "pgmaster",
                    "size": null,
                    "status": "FAILED",
                    "systemid": "6847607985520892865",
                    "tablespaces": null,
                    "timeline": 1,
                    "version": 110008,
                    "xlog_segment_size": 16777216
                },
                "20200712T184527": {
                    "backup_id": "20200712T184527",
                    "backup_label": null,
                    "begin_offset": 96,
                    "begin_time": "Sun Jul 12 18:45:26 2020",
                    "begin_wal": "00000001000000000000003C",
                    "begin_xlog": "0/3C000060",
                    "config_file": "/var/lib/pgsql/11/data/postgresql.conf",
                    "copy_stats": null,
                    "deduplicated_size": null,
                    "end_offset": null,
                    "end_time": null,
                    "end_wal": null,
                    "end_xlog": null,
                    "error": "failure copying files (KeyboardInterrupt)",
                    "hba_file": "/var/lib/pgsql/11/data/pg_hba.conf",
                    "ident_file": "/var/lib/pgsql/11/data/pg_ident.conf",
                    "included_files": null,
                    "mode": "postgres",
                    "pgdata": "/var/lib/pgsql/11/data",
                    "server_name": "pgmaster",
                    "size": null,
                    "status": "FAILED",
                    "systemid": "6847607985520892865",
                    "tablespaces": null,
                    "timeline": 1,
                    "version": 110008,
                    "xlog_segment_size": 16777216
                },
                "20200712T233449": {
                    "backup_id": "20200712T233449",
                    "backup_label": null,
                    "begin_offset": 320,
                    "begin_time": "Sun Jul 12 23:34:48 2020",
                    "begin_wal": "00000001000000000000003E",
                    "begin_xlog": "0/3E000140",
                    "config_file": "/var/lib/pgsql/11/data/postgresql.conf",
                    "copy_stats": null,
                    "deduplicated_size": null,
                    "end_offset": null,
                    "end_time": null,
                    "end_wal": null,
                    "end_xlog": null,
                    "error": "failure copying files (KeyboardInterrupt)",
                    "hba_file": "/var/lib/pgsql/11/data/pg_hba.conf",
                    "ident_file": "/var/lib/pgsql/11/data/pg_ident.conf",
                    "included_files": null,
                    "mode": "postgres",
                    "pgdata": "/var/lib/pgsql/11/data",
                    "server_name": "pgmaster",
                    "size": null,
                    "status": "FAILED",
                    "systemid": "6847607985520892865",
                    "tablespaces": null,
                    "timeline": 1,
                    "version": 110008,
                    "xlog_segment_size": 16777216
                },
                "20200713T010923": {
                    "backup_id": "20200713T010923",
                    "backup_label": null,
                    "begin_offset": 320,
                    "begin_time": "Mon Jul 13 01:09:23 2020",
                    "begin_wal": "000000010000000000000040",
                    "begin_xlog": "0/40000140",
                    "config_file": "/var/lib/pgsql/11/data/postgresql.conf",
                    "copy_stats": null,
                    "deduplicated_size": null,
                    "end_offset": null,
                    "end_time": null,
                    "end_wal": null,
                    "end_xlog": null,
                    "error": "failure copying files (KeyboardInterrupt)",
                    "hba_file": "/var/lib/pgsql/11/data/pg_hba.conf",
                    "ident_file": "/var/lib/pgsql/11/data/pg_ident.conf",
                    "included_files": null,
                    "mode": "postgres",
                    "pgdata": "/var/lib/pgsql/11/data",
                    "server_name": "pgmaster",
                    "size": null,
                    "status": "FAILED",
                    "systemid": "6847607985520892865",
                    "tablespaces": null,
                    "timeline": 1,
                    "version": 110008,
                    "xlog_segment_size": 16777216
                },
                "20200713T010951": {
                    "backup_id": "20200713T010951",
                    "backup_label": null,
                    "begin_offset": 96,
                    "begin_time": "Mon Jul 13 01:09:51 2020",
                    "begin_wal": "000000010000000000000042",
                    "begin_xlog": "0/42000060",
                    "config_file": "/var/lib/pgsql/11/data/postgresql.conf",
                    "copy_stats": null,
                    "deduplicated_size": null,
                    "end_offset": null,
                    "end_time": null,
                    "end_wal": null,
                    "end_xlog": null,
                    "error": "failure copying files (KeyboardInterrupt)",
                    "hba_file": "/var/lib/pgsql/11/data/pg_hba.conf",
                    "ident_file": "/var/lib/pgsql/11/data/pg_ident.conf",
                    "included_files": null,
                    "mode": "postgres",
                    "pgdata": "/var/lib/pgsql/11/data",
                    "server_name": "pgmaster",
                    "size": null,
                    "status": "FAILED",
                    "systemid": "6847607985520892865",
                    "tablespaces": null,
                    "timeline": 1,
                    "version": 110008,
                    "xlog_segment_size": 16777216
                },
                "20200713T011334": {
                    "backup_id": "20200713T011334",
                    "backup_label": null,
                    "begin_offset": 96,
                    "begin_time": "Mon Jul 13 01:13:34 2020",
                    "begin_wal": "000000010000000000000044",
                    "begin_xlog": "0/44000060",
                    "config_file": "/var/lib/pgsql/11/data/postgresql.conf",
                    "copy_stats": null,
                    "deduplicated_size": null,
                    "end_offset": null,
                    "end_time": null,
                    "end_wal": null,
                    "end_xlog": null,
                    "error": "failure copying files (KeyboardInterrupt)",
                    "hba_file": "/var/lib/pgsql/11/data/pg_hba.conf",
                    "ident_file": "/var/lib/pgsql/11/data/pg_ident.conf",
                    "included_files": null,
                    "mode": "postgres",
                    "pgdata": "/var/lib/pgsql/11/data",
                    "server_name": "pgmaster",
                    "size": null,
                    "status": "FAILED",
                    "systemid": "6847607985520892865",
                    "tablespaces": null,
                    "timeline": 1,
                    "version": 110008,
                    "xlog_segment_size": 16777216
                },
                "20200713T011521": {
                    "backup_id": "20200713T011521",
                    "backup_label": null,
                    "begin_offset": 96,
                    "begin_time": "Mon Jul 13 01:15:21 2020",
                    "begin_wal": "000000010000000000000047",
                    "begin_xlog": "0/47000060",
                    "config_file": "/var/lib/pgsql/11/data/postgresql.conf",
                    "copy_stats": null,
                    "deduplicated_size": null,
                    "end_offset": null,
                    "end_time": null,
                    "end_wal": null,
                    "end_xlog": null,
                    "error": "failure copying files (KeyboardInterrupt)",
                    "hba_file": "/var/lib/pgsql/11/data/pg_hba.conf",
                    "ident_file": "/var/lib/pgsql/11/data/pg_ident.conf",
                    "included_files": null,
                    "mode": "postgres",
                    "pgdata": "/var/lib/pgsql/11/data",
                    "server_name": "pgmaster",
                    "size": null,
                    "status": "FAILED",
                    "systemid": "6847607985520892865",
                    "tablespaces": null,
                    "timeline": 1,
                    "version": 110008,
                    "xlog_segment_size": 16777216
                },
                "20200713T022118": {
                    "backup_id": "20200713T022118",
                    "backup_label": null,
                    "begin_offset": 96,
                    "begin_time": "Mon Jul 13 02:21:18 2020",
                    "begin_wal": "00000001000000000000004E",
                    "begin_xlog": "0/4E000060",
                    "config_file": "/var/lib/pgsql/11/data/postgresql.conf",
                    "copy_stats": null,
                    "deduplicated_size": null,
                    "end_offset": null,
                    "end_time": null,
                    "end_wal": null,
                    "end_xlog": null,
                    "error": "failure copying files (data transfer failure on directory '/var/lib/barman/pgmaster/base/20200713T022118/data')",
                    "hba_file": "/var/lib/pgsql/11/data/pg_hba.conf",
                    "ident_file": "/var/lib/pgsql/11/data/pg_ident.conf",
                    "included_files": null,
                    "mode": "postgres",
                    "pgdata": "/var/lib/pgsql/11/data",
                    "server_name": "pgmaster",
                    "size": null,
                    "status": "FAILED",
                    "systemid": "6847607985520892865",
                    "tablespaces": null,
                    "timeline": 1,
                    "version": 110008,
                    "xlog_segment_size": 16777216
                },
                "20200713T022813": {
                    "backup_id": "20200713T022813",
                    "backup_label": null,
                    "begin_offset": 208,
                    "begin_time": "Mon Jul 13 02:28:13 2020",
                    "begin_wal": "000000010000000000000051",
                    "begin_xlog": "0/510000D0",
                    "config_file": "/var/lib/pgsql/11/data/postgresql.conf",
                    "copy_stats": null,
                    "deduplicated_size": null,
                    "end_offset": null,
                    "end_time": null,
                    "end_wal": null,
                    "end_xlog": null,
                    "error": "failure copying files (KeyboardInterrupt)",
                    "hba_file": "/var/lib/pgsql/11/data/pg_hba.conf",
                    "ident_file": "/var/lib/pgsql/11/data/pg_ident.conf",
                    "included_files": null,
                    "mode": "postgres",
                    "pgdata": "/var/lib/pgsql/11/data",
                    "server_name": "pgmaster",
                    "size": null,
                    "status": "FAILED",
                    "systemid": "6847607985520892865",
                    "tablespaces": null,
                    "timeline": 1,
                    "version": 110008,
                    "xlog_segment_size": 16777216
                },
                "20200713T081402": {
                    "backup_id": "20200713T081402",
                    "backup_label": null,
                    "begin_offset": 320,
                    "begin_time": "Mon Jul 13 08:14:01 2020",
                    "begin_wal": "000000010000000000000054",
                    "begin_xlog": "0/54000140",
                    "config_file": "/var/lib/pgsql/11/data/postgresql.conf",
                    "copy_stats": null,
                    "deduplicated_size": null,
                    "end_offset": null,
                    "end_time": null,
                    "end_wal": null,
                    "end_xlog": null,
                    "error": "failure copying files (KeyboardInterrupt)",
                    "hba_file": "/var/lib/pgsql/11/data/pg_hba.conf",
                    "ident_file": "/var/lib/pgsql/11/data/pg_ident.conf",
                    "included_files": null,
                    "mode": "postgres",
                    "pgdata": "/var/lib/pgsql/11/data",
                    "server_name": "pgmaster",
                    "size": null,
                    "status": "FAILED",
                    "systemid": "6847607985520892865",
                    "tablespaces": null,
                    "timeline": 1,
                    "version": 110008,
                    "xlog_segment_size": 16777216
                },
                "20200713T090056": {
                    "backup_id": "20200713T090056",
                    "backup_label": null,
                    "begin_offset": 96,
                    "begin_time": "Mon Jul 13 09:00:55 2020",
                    "begin_wal": "000000010000000000000058",
                    "begin_xlog": "0/58000060",
                    "config_file": "/var/lib/pgsql/11/data/postgresql.conf",
                    "copy_stats": null,
                    "deduplicated_size": null,
                    "end_offset": null,
                    "end_time": null,
                    "end_wal": null,
                    "end_xlog": null,
                    "error": "failure copying files (KeyboardInterrupt)",
                    "hba_file": "/var/lib/pgsql/11/data/pg_hba.conf",
                    "ident_file": "/var/lib/pgsql/11/data/pg_ident.conf",
                    "included_files": null,
                    "mode": "postgres",
                    "pgdata": "/var/lib/pgsql/11/data",
                    "server_name": "pgmaster",
                    "size": null,
                    "status": "FAILED",
                    "systemid": "6847607985520892865",
                    "tablespaces": null,
                    "timeline": 1,
                    "version": 110008,
                    "xlog_segment_size": 16777216
                },
                "20200713T124758": {
                    "backup_id": "20200713T124758",
                    "backup_label": null,
                    "begin_offset": 320,
                    "begin_time": "Mon Jul 13 12:47:58 2020",
                    "begin_wal": "00000001000000000000005A",
                    "begin_xlog": "0/5A000140",
                    "config_file": "/var/lib/pgsql/11/data/postgresql.conf",
                    "copy_stats": null,
                    "deduplicated_size": null,
                    "end_offset": null,
                    "end_time": null,
                    "end_wal": null,
                    "end_xlog": null,
                    "error": "failure copying files (KeyboardInterrupt)",
                    "hba_file": "/var/lib/pgsql/11/data/pg_hba.conf",
                    "ident_file": "/var/lib/pgsql/11/data/pg_ident.conf",
                    "included_files": null,
                    "mode": "postgres",
                    "pgdata": "/var/lib/pgsql/11/data",
                    "server_name": "pgmaster",
                    "size": null,
                    "status": "FAILED",
                    "systemid": "6847607985520892865",
                    "tablespaces": null,
                    "timeline": 1,
                    "version": 110008,
                    "xlog_segment_size": 16777216
                }
            },
            "config": {
                "active": true,
                "archiver": true,
                "archiver_batch_size": 0,
                "backup_directory": "/var/lib/barman/pgmaster",
                "backup_method": "postgres",
                "backup_options": "concurrent_backup",
                "bandwidth_limit": null,
                "barman_home": "/var/lib/barman",
                "barman_lock_directory": "/var/lib/barman",
                "basebackup_retry_sleep": 30,
                "basebackup_retry_times": 0,
                "basebackups_directory": "/var/lib/barman/pgmaster/base",
                "check_timeout": 30,
                "compression": "gzip",
                "conninfo": "host=pgmaster port=5432 user=barman dbname=postgres",
                "create_slot": "manual",
                "custom_compression_filter": null,
                "custom_decompression_filter": null,
                "description": "Master backup",
                "disabled": false,
                "errors_directory": "/var/lib/barman/pgmaster/errors",
                "immediate_checkpoint": false,
                "incoming_wals_directory": "/var/lib/barman/pgmaster/incoming",
                "last_backup_maximum_age": null,
                "max_incoming_wals_queue": null,
                "minimum_redundancy": 5,
                "msg_list": [],
                "name": "pgmaster",
                "network_compression": false,
                "parallel_jobs": 1,
                "path_prefix": null,
                "post_archive_retry_script": null,
                "post_archive_script": null,
                "post_backup_retry_script": null,
                "post_backup_script": null,
                "post_delete_retry_script": null,
                "post_delete_script": null,
                "post_recovery_retry_script": null,
                "post_recovery_script": null,
                "post_wal_delete_retry_script": null,
                "post_wal_delete_script": null,
                "pre_archive_retry_script": null,
                "pre_archive_script": null,
                "pre_backup_retry_script": null,
                "pre_backup_script": null,
                "pre_delete_retry_script": null,
                "pre_delete_script": null,
                "pre_recovery_retry_script": null,
                "pre_recovery_script": null,
                "pre_wal_delete_retry_script": null,
                "pre_wal_delete_script": null,
                "primary_ssh_command": null,
                "recovery_options": "get-wal",
                "retention_policy": "window 7 d",
                "retention_policy_mode": "auto",
                "reuse_backup": null,
                "slot_name": "barman",
                "ssh_command": null,
                "streaming_archiver": true,
                "streaming_archiver_batch_size": 0,
                "streaming_archiver_name": "barman_receive_wal",
                "streaming_backup_name": "barman_streaming_backup",
                "streaming_conninfo": "host=pgmaster port=5432 user=streaming_barman dbname=postgres",
                "streaming_wals_directory": "/var/lib/barman/pgmaster/streaming",
                "tablespace_bandwidth_limit": null,
                "wal_retention_policy": "simple-wal 7 d",
                "wals_directory": "/var/lib/barman/pgmaster/wals"
            },
            "status": {
                "archive_command": "barman-wal-archive backup pgmaster %p",
                "archive_mode": "on",
                "archive_timeout": 0,
                "archived_count": 0,
                "checkpoint_timeout": 300,
                "config_file": "/var/lib/pgsql/11/data/postgresql.conf",
                "connection_error": null,
                "current_archived_wals_per_second": 0.0,
                "current_lsn": "0/5C000060",
                "current_size": 40953029.0,
                "current_xlog": "00000001000000000000005C",
                "data_checksums": "off",
                "data_directory": "/var/lib/pgsql/11/data",
                "failed_count": 5795,
                "has_backup_privileges": true,
                "hba_file": "/var/lib/pgsql/11/data/pg_hba.conf",
                "hot_standby": "on",
                "ident_file": "/var/lib/pgsql/11/data/pg_ident.conf",
                "is_archiving": null,
                "is_in_recovery": false,
                "is_superuser": true,
                "last_archived_time": null,
                "last_archived_wal": null,
                "last_failed_time": "Mon Jul 13 12:48:03 2020",
                "last_failed_wal": "000000010000000000000021",
                "max_replication_slots": "4",
                "max_wal_senders": "8",
                "pg_basebackup_bwlimit": true,
                "pg_basebackup_compatible": true,
                "pg_basebackup_installed": true,
                "pg_basebackup_path": "/bin/pg_basebackup",
                "pg_basebackup_tbls_mapping": true,
                "pg_basebackup_version": "11.8",
                "pg_receivexlog_compatible": true,
                "pg_receivexlog_installed": true,
                "pg_receivexlog_path": "/usr/pgsql-11/bin/pg_receivewal",
                "pg_receivexlog_supports_slots": true,
                "pg_receivexlog_synchronous": false,
                "pg_receivexlog_version": "11.8",
                "pgespresso_installed": false,
                "postgres_systemid": "6847607985520892865",
                "replication_slot": [
                    "barman",
                    true,
                    "0/5C000000"
                ],
                "replication_slot_support": true,
                "server_txt_version": "11.8",
                "stats_reset": "Fri Jul 10 01:16:34 2020",
                "streaming": true,
                "streaming_supported": true,
                "streaming_systemid": "6847607985520892865",
                "synchronous_standby_names": [
                    ""
                ],
                "timeline": 1,
                "wal_compression": "off",
                "wal_keep_segments": "6666660",
                "wal_level": "replica",
                "xlog_segment_size": 16777216,
                "xlogpos": "0/5C000060"
            },
            "wals": {
                "last_archived_wal_per_timeline": {
                    "00000001": {
                        "compression": "gzip",
                        "name": "00000001000000000000005B",
                        "size": 16463,
                        "time": 1594633679.936722
                    }
                }
            }
        }
    }
}
```

В логах barman:

```
2020-07-13 12:49:02,668 [24734] barman.server INFO: Another cron process is already running on server pgmaster. Skipping to the next server
2020-07-13 12:49:03,094 [24735] barman.wal_archiver INFO: No xlog segments found from streaming for pgmaster.
2020-07-13 12:49:03,095 [24735] barman.wal_archiver INFO: No xlog segments found from file archival for pgmaster.
2020-07-13 12:49:50,173 [24784] barman.server INFO: Ignoring failed check 'failed backups' for server 'pgmaster'
2020-07-13 12:49:50,173 [24784] barman.server INFO: Ignoring failed check 'minimum redundancy requirements' for server 'pgmaster'
2020-07-13 12:49:50,209 [24784] barman.backup INFO: Starting backup using postgres method for server pgmaster in /var/lib/barman/pgmaster/base/20200713T124950
2020-07-13 12:49:50,231 [24784] barman.backup_executor INFO: Backup start at LSN: 0/5C000060 (00000001000000000000005C, 00000060)
2020-07-13 12:49:50,234 [24784] barman.backup_executor INFO: Starting backup copy via pg_basebackup for 20200713T124950
2020-07-13 12:49:50,539 [18519] barman.command_wrappers INFO: pgmaster: pg_receivewal: finished segment at 0/5D000000
(timeline 1)
2020-07-13 12:49:51,526 [18519] barman.command_wrappers INFO: pgmaster: pg_receivewal: finished segment at 0/5E000000
(timeline 1)
2020-07-13 12:49:59,102 [24784] barman.backup ERROR: Backup failed copying files.
DETAILS: KeyboardInterrupt
2020-07-13 12:49:59,111 [24784] barman.wal_archiver INFO: Found 1 xlog segments from streaming for pgmaster. Archive all segments in one run.
2020-07-13 12:49:59,111 [24784] barman.wal_archiver INFO: Archiving segment 1 of 1 from streaming: pgmaster/00000001000000000000005C
2020-07-13 12:49:59,296 [24784] barman.wal_archiver INFO: No xlog segments found from file archival for pgmaster.
```

В логах pgmaster:

```
[root@pgmaster data]# tail -n 50 log/postgresql-Mon.log
2020-07-13 12:49:50.849 MSK [12370] DEBUG:  file "pg_internal.init" excluded from backup
2020-07-13 12:49:50.967 MSK [12370] DEBUG:  file "pg_internal.init" excluded from backup
2020-07-13 12:49:51.103 MSK [12370] DEBUG:  contents of directory "pg_replslot" excluded from backup
2020-07-13 12:49:51.103 MSK [12370] DEBUG:  contents of directory "pg_stat_tmp" excluded from backup
2020-07-13 12:49:51.205 MSK [12370] DEBUG:  file "postmaster.opts" excluded from backup
2020-07-13 12:49:51.205 MSK [12370] DEBUG:  file "postmaster.pid" excluded from backup
ERROR: Error executing ssh: [Errno 32] Broken pipe
Exception ValueError: 'I/O operation on closed file' in <bound method _Stream.__del__ of <tarfile._Stream instance at
0x7fe7601348c0>> ignored
2020-07-13 12:49:51.529 MSK [6089] LOG:  archive command failed with exit code 2
2020-07-13 12:49:51.529 MSK [6089] DETAIL:  The failed archive command was: barman-wal-archive backup pgmaster pg_wal/000000010000000000000021
2020-07-13 12:49:57.268 MSK [12370] NOTICE:  pg_stop_backup cleanup done, waiting for required WAL segments to be archived
ERROR: Error executing ssh: [Errno 32] Broken pipe
Exception ValueError: 'I/O operation on closed file' in <bound method _Stream.__del__ of <tarfile._Stream instance at
0x7fe1d412f8c0>> ignored
2020-07-13 12:49:57.747 MSK [6089] LOG:  archive command failed with exit code 2
2020-07-13 12:49:57.747 MSK [6089] DETAIL:  The failed archive command was: barman-wal-archive backup pgmaster pg_wal/000000010000000000000021
2020-07-13 12:49:57.747 MSK [6089] WARNING:  archiving write-ahead log file "000000010000000000000021" failed too many times, will try again later
ERROR: Error executing ssh: [Errno 32] Broken pipe
Exception ValueError: 'I/O operation on closed file' in <bound method _Stream.__del__ of <tarfile._Stream instance at
0x7f4c6a9458c0>> ignored
2020-07-13 12:49:57.919 MSK [6089] LOG:  archive command failed with exit code 2
2020-07-13 12:49:57.919 MSK [6089] DETAIL:  The failed archive command was: barman-wal-archive backup pgmaster pg_wal/000000010000000000000021
ERROR: Error executing ssh: [Errno 32] Broken pipe
Exception ValueError: 'I/O operation on closed file' in <bound method _Stream.__del__ of <tarfile._Stream instance at
0x7ffa3f3de8c0>> ignored
2020-07-13 12:49:59.090 MSK [6089] LOG:  archive command failed with exit code 2
2020-07-13 12:49:59.090 MSK [6089] DETAIL:  The failed archive command was: barman-wal-archive backup pgmaster pg_wal/000000010000000000000021
2020-07-13 12:49:59.803 MSK [12244] WARNING:  pg_stop_backup still waiting for all required WAL segments to be archived (120 seconds elapsed)
2020-07-13 12:49:59.803 MSK [12244] HINT:  Check that your archive_command is executing properly.  pg_stop_backup can
be canceled safely, but the database backup will not be usable without all the WAL segments.
2020-07-13 12:49:59.803 MSK [12244] LOG:  could not send data to client: Broken pipe
2020-07-13 12:49:59.803 MSK [12244] FATAL:  connection to client lost
ERROR: Error executing ssh: [Errno 32] Broken pipe
Exception ValueError: 'I/O operation on closed file' in <bound method _Stream.__del__ of <tarfile._Stream instance at
0x7f24a0be98c0>> ignored
2020-07-13 12:50:00.273 MSK [6089] LOG:  archive command failed with exit code 2
2020-07-13 12:50:00.273 MSK [6089] DETAIL:  The failed archive command was: barman-wal-archive backup pgmaster pg_wal/000000010000000000000021
2020-07-13 12:50:00.273 MSK [6089] WARNING:  archiving write-ahead log file "000000010000000000000021" failed too many times, will try again later
2020-07-13 12:50:06.794 MSK [12402] DEBUG:  autovacuum: processing database "postgres"
2020-07-13 12:50:36.930 MSK [12427] DEBUG:  autovacuum: processing database "test"
2020-07-13 12:50:51.256 MSK [12370] WARNING:  pg_stop_backup still waiting for all required WAL segments to be archived (60 seconds elapsed)
2020-07-13 12:50:51.256 MSK [12370] HINT:  Check that your archive_command is executing properly.  pg_stop_backup can
be canceled safely, but the database backup will not be usable without all the WAL segments.
ERROR: Error executing ssh: [Errno 32] Broken pipe
Exception ValueError: 'I/O operation on closed file' in <bound method _Stream.__del__ of <tarfile._Stream instance at
0x7fb81f15e8c0>> ignored
2020-07-13 12:51:00.454 MSK [6089] LOG:  archive command failed with exit code 2
2020-07-13 12:51:00.454 MSK [6089] DETAIL:  The failed archive command was: barman-wal-archive backup pgmaster pg_wal/000000010000000000000021
ERROR: Error executing ssh: [Errno 32] Broken pipe
Exception ValueError: 'I/O operation on closed file' in <bound method _Stream.__del__ of <tarfile._Stream instance at
0x7f9f645688c0>> ignored
2020-07-13 12:51:01.644 MSK [6089] LOG:  archive command failed with exit code 2
2020-07-13 12:51:01.644 MSK [6089] DETAIL:  The failed archive command was: barman-wal-archive backup pgmaster pg_wal/000000010000000000000021
ERROR: Error executing ssh: [Errno 32] Broken pipe
Exception ValueError: 'I/O operation on closed file' in <bound method _Stream.__del__ of <tarfile._Stream instance at
0x7fe209ead8c0>> ignored
2020-07-13 12:51:02.826 MSK [6089] LOG:  archive command failed with exit code 2
2020-07-13 12:51:02.826 MSK [6089] DETAIL:  The failed archive command was: barman-wal-archive backup pgmaster pg_wal/000000010000000000000021
2020-07-13 12:51:02.826 MSK [6089] WARNING:  archiving write-ahead log file "000000010000000000000021" failed too many times, will try again later
```





<details><summary>Дальше рыбу заворачивал</summary>
ssh -o "UserKnownHostsFile=/dev/null" -o "StrictHostKeyChecking=no" user@host


Проверяем репликацию

На мастере
postgres=# select * from pg_stat_replication;
 pid | usesysid | usename | application_name | client_addr | client_hostname | client_port | backend_start | backend_xmin | state | sent_lsn | write_lsn | flush_lsn | replay_lsn | write_lag
| flush_lag | replay_lag | sync_priority | sync_state
-----+----------+---------+------------------+-------------+-----------------+-------------+---------------+--------------+-------+----------+-----------+-----------+------------+-----------+-----------+------------+---------------+------------
(0 rows)

На слейве
postgres=# select * from pg_stat_wal_receiver;
 pid | status | receive_start_lsn | receive_start_tli | received_lsn | received_tli | last_msg_send_time | last_msg_receipt_time | latest_end_lsn | latest_end_time | slot_name | sender_host
| sender_port | conninfo
-----+--------+-------------------+-------------------+--------------+--------------+--------------------+-----------------------+----------------+-----------------+-----------+-------------+-------------+----------
(0 rows)



На слейве:
1. /usr/pgsql-11/bin/postgresql-11-setup initdb
2. Очистить содержимое /var/lib/pgsql/11/data/
3. Сделать бэкап postgresql.conf, pg_hba.conf, recovery.conf

На мастере
4. postgres=# select pg_start_backup('replication-setup',true);

На слейве
5. sudo -u postgres pg_basebackup -D /var/lib/pgsql/11/data -R -X stream -c fast -P -d 'host=192.168.11.20 user=replication'

После этого процесс postgresql на слейве упадет, если заведомо не будет подходящим образом сконфигурирован pg_hba.conf мастера, в этом случае надо вернуть конфиги слейва на место.

На мастере
6. postgres=# select pg_stop_backup();

На слейве
7. systemctl start postgresql-11


Проверяем
На мастере
postgres=# select * from pg_stat_replication;
  pid  | usesysid |   usename   | application_name |  client_addr  | client_hostname | client_port |         backend_start         | backend_xmin |   state   |  sent_lsn  | write_lsn  | flush_lsn  | replay_lsn | write_lag | flush_lag | replay_lag | sync_priority | sync_state
-------+----------+-------------+------------------+---------------+-----------------+-------------+-------------------------------+--------------+-----------+------------+------------+------------+------------+-----------+-----------+------------+---------------+------------
 31117 |    16384 | replication | walreceiver      | 192.168.11.21 |                 |       37132 | 2020-07-11 01:55:35.162275+03 |              | streaming | 0/20000060 | 0/20000060 | 0/20000060 | 0/20000060 |           |           |            |             0 | async
(1 row)


На слейве
postgres=# select * from pg_stat_wal_receiver;
  pid  |  status   | receive_start_lsn | receive_start_tli | received_lsn | received_tli |
 last_msg_send_time       |     last_msg_receipt_time     | latest_end_lsn |        latest_end_time        |  slot_name   |  sender_host  | sender_port |
                                                          conninfo

-------+-----------+-------------------+-------------------+--------------+--------------+-------------------------------+-------------------------------+----------------+-------------------------------+--------------+---------------+-------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 24808 | streaming | 0/1F000000        |                 1 | 0/20000060   |            1 | 2020-07-11 01:56:18.643987+03 | 2020-07-11 01:56:18.644719+03 | 0/20000060     | 2020-07-11 01:55:48.597915+03 | standby_slot | 192.168.11.20 |        5432 | user=replication password=******** dbname=replication host=192.168.11.20 port=5432 fallback_application_name=walreceiver sslmode=prefer sslcompression=0 krbsrvname=postgres target_session_attrs=any
(1 row)


На мастере
postgres=# create database test222;
CREATE DATABASE

На слейве
postgres=# \l
                                  List of databases
   Name    |  Owner   | Encoding |   Collate   |    Ctype    |   Access privileges
-----------+----------+----------+-------------+-------------+-----------------------
 demo      | postgres | UTF8     | en_US.UTF-8 | en_US.UTF-8 |
 postgres  | postgres | UTF8     | en_US.UTF-8 | en_US.UTF-8 |
 template0 | postgres | UTF8     | en_US.UTF-8 | en_US.UTF-8 | =c/postgres          +
           |          |          |             |             | postgres=CTc/postgres
 template1 | postgres | UTF8     | en_US.UTF-8 | en_US.UTF-8 | =c/postgres          +
           |          |          |             |             | postgres=CTc/postgres
 test      | postgres | UTF8     | en_US.UTF-8 | en_US.UTF-8 |
 test222   | postgres | UTF8     | en_US.UTF-8 | en_US.UTF-8 |
(6 rows)


archive_mode    = on
archive_command = 'cp %p /var/lib/pgsql/11/backups/%f'

5 0 * * * find /var/lib/pgsql/11/backups/ -mtime +7 -exec rm -f {} \;






Barman


barman show-server pgmaster
barman receive-wal --create-slot pgmaster
barman receive-wal pgmaster
barman check pgmaster

cat > /var/lib/barman/.pgpass
chmod 0600 /var/lib/barman/.pgpass


export PATH=$PATH:/usr/pgsql-11/bin


barman switch-wal pgmaster

если не срабатывает, то:

barman reset pgmaster

и потом снова 

barman switch-wal pgmaster




barman switch-wal --force --archive pgmaster

и затем снова 

barman backup pgmaster
</details>