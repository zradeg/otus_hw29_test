

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