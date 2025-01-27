<a href="https://zerodha.tech"><img src="https://zerodha.tech/static/images/github-badge.svg" align="right" /></a>

![listmonk](https://user-images.githubusercontent.com/547147/89733021-43fbf700-da70-11ea-82e4-e98cb5010257.png)

listmonk is a standalone, self-hosted, newsletter and mailing list manager. It is fast, feature-rich, and packed into a single binary. It uses a PostgreSQL database as its data store.

[![listmonk-dashboard](https://user-images.githubusercontent.com/547147/89733057-87566580-da70-11ea-8160-855f6f046a55.png)](https://listmonk.app)
Visit [listmonk.app](https://listmonk.app)

## Installation

### Docker

The latest image is available on DockerHub at `listmonk/listmonk:latest`. Use the sample [docker-compose.yml](https://github.com/knadh/listmonk/blob/master/docker-compose.yml) to run listmonk and Postgres DB with docker-compose as follows:

#### Demo

```bash
mkdir listmonk-demo && cd listmonk-demo
sh -c "$(curl -fsSL https://raw.githubusercontent.com/knadh/listmonk/master/install-demo.sh)"
```

The demo does not persist Postgres after the containers are removed. DO NOT use this demo setup in production.

#### Production

##### Easy Docker install

This setup is recommended if you want to _quickly_ setup `listmonk` in production.

```bash
mkdir listmonk && cd listmonk
sh -c "$(curl -fsSL https://raw.githubusercontent.com/knadh/listmonk/master/install-prod.sh)"
```

The above shell script performs the following actions:

- Downloads `docker-compose.yml` and generates a `config.toml`.
- Runs a Postgres container and installs the database schema.
- Runs the `listmonk` container.

**NOTE**: It's recommended to examine the contents of the shell script, before running in your environment.

##### Manual Docker install

The following workflow is recommended to setup `listmonk` manually using `docker-compose`. You are encouraged to customise the contents of `docker-compose.yml` to your needs. The overall setup looks like:

- `docker-compose up db` to run the Postgres DB.
- `docker-compose run --rm app ./listmonk --install` to setup the DB (or `--upgrade` to upgrade an existing DB).
- Copy `config.toml.sample` to your directory and make the following changes:
    - `app.address` => `0.0.0.0:9000` (Port forwarding on Docker will work only if the app is advertising on all interfaces.)
    - `db.host` => `listmonk_db` (Container Name of the DB container)
- Run `docker-compose up app` and visit `http://localhost:9000`.

More information on [docs](https://listmonk.app/docs).

__________________

### Binary
- Download the [latest release](https://github.com/knadh/listmonk/releases) and extract the listmonk binary.
- `./listmonk --new-config` to generate config.toml. Then, edit the file.
- `./listmonk --install` to setup the Postgres DB (or `--upgrade` to upgrade an existing DB. Upgrades are idempotent and running them multiple times have no side effects).
- Run `./listmonk` and visit `http://localhost:9000`.

__________________

### Heroku 
[![Deploy](https://www.herokucdn.com/deploy/button.svg)](https://heroku.com/deploy?template=https://github.com/knadh/listmonk-heroku)


## Developers
listmonk is a free and open source software licensed under AGPLv3. If you are interested in contributing, refer to the [developer setup](https://listmonk.app/docs/developer-setup). The backend is written in Go and the frontend is Vue with Buefy for UI. 


## License
listmonk is licensed under the AGPL v3 license.
