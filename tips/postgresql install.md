# [§](https://lobotuerto.com/blog/how-to-install-postgresql-in-manjaro-linux/#installation-process) Installation process

Setting up **PostgreSQL** in **Manjaro Linux** is very easy.

Just follow these steps and you’ll have a working installation in no time.

Install the `postgresql` package:

```bash
sudo pacman -S postgresql postgis
```

Switch to the `postgres` user account and initialize the database cluster:

```bash
sudo su postgres -l # or sudo -u postgres -i
initdb --locale $LANG -E UTF8 -D '/var/lib/postgres/data/'
exit
```

Options for `initdb` are as follows:

- `--locale` is the one defined in `/etc/locale.conf`.
- `-E` is the default encoding for new databases.
- `-D` is the default location for storing the database cluster.

Now, start and enable the `postgresql.service`:

```bash
sudo systemctl enable --now postgresql.service
```

You can check PostgreSQL’s version with:

```bash
psql --version
# psql (PostgreSQL) 12.2
```

## [§](https://lobotuerto.com/blog/how-to-install-postgresql-in-manjaro-linux/#create-a-db-user-for-local-development-or-deployment) Create a DB user for local development or deployment

```bash
psql -U postgres
CREATE USER deployer WITH PASSWORD 'eldeployerloco';
ALTER ROLE deployer WITH CREATEDB;
\q
```

On **Phoenix** you’d use this in `config/dev.exs` like this:

```elixir
# Configure your database
config :my_app, MyApp.Repo,
  username: "deployer",
  password: "eldeployerloco",
  database: "my_app_dev",
  hostname: "localhost",
  show_sensitive_data_on_connection_error: true,
  pool_size: 10
```

That’s it!

# [§](https://lobotuerto.com/blog/how-to-install-postgresql-in-manjaro-linux/#links) Links

- [ArchWiki – PostgreSQL](https://wiki.archlinux.org/index.php/PostgreSQL)
- [ArchWiki – systemd](https://wiki.archlinux.org/index.php/Systemd)