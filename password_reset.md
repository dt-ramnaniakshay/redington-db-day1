# resetting password / allowing user to login

1. \du

2. check if user is present or not

3. check the file `/etc/postgresql/<version>/main/pg_hba.conf or /var/lib/pgsql/data/pg_hba.conf` and make some changes over there

4. you will see something like this
```
local   all             all                                     peer
```

change it to this

```
local   all             all                                     md5
```

5. restart your services

```bash
sudo service postgresql restart
sudo systemctl restart postgresql
```
- now login with your role

```bash
psql -U developer -d your_database
```