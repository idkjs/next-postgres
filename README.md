# next-postgres

This is an example of a web application with posts, comments and server side rendering. It is configured to be deployed to [Zeit](https://zeit.co). It is code you can use without attribution, please enjoy.

- [Maurice Kenji Clarke](https://twitter.com/mauricekenji) used the setup to create: [https://indvstry.io/](https://indvstry.io/)
- I built [Reading Supply](https://reading.supply/@jim) after modifing the setup and removing Sequelize for [Knex](https://knexjs.org/).

An old ugly preview is available [here](https://next-postgres.herokuapp.com/).

**Stack**

- [NextJS + Custom Express](https://github.com/zeit/next.js/)
- [Emotion CSS-in-JS](https://github.com/emotion-js/emotion)
- [Postgres](https://www.postgresql.org/)
- [Sequelize: PostgresSQL ORM](http://docs.sequelizejs.com/)
- [Passport for local authentication](http://passportjs.org/)
- [Redux](http://redux.js.org/)
- [Babel](https://babeljs.io/)

**Why is this useful? Why should I care?**

- The UX and UI are garbage, that means everything you do after will be better!
- Client and server are written in JavaScript.
- This is a production ready codebase you can use to test a concept you have.
- [Server side rendering](https://zeit.co/blog/next2) has been made simple.
- Maybe you want to get a head start at a hackathon.

## Setup: Prerequisites

I use [Homebrew](https://brew.sh/) to manage dependencies on a new laptop... You're welcome to use something else.

- Install Postgres: `brew install postgres`.
- Install [Node 10+](https://nodejs.org/en/): `brew install node`. (Or update your node)

## Setup: Quick newbies guide to Postgres

- On OSX, to run Postgres in a tab on the default port.

```sh
postgres -D /usr/local/var/postgres -p 5432
```

- Postgres config is stored in `./config.js`.
- Local database: `nextdb`.
- Username and password as `test`.

### First time Postgres instructions.

```sh
# Enter Postgres console
psql postgres

# Create a new user for yourself
CREATE ROLE yourname WITH LOGIN PASSWORD 'yourname';

# Allow yourself to create databases
ALTER ROLE yourname CREATEDB;

# Exit Postgres console
\q

# Log in as your new user.
psql postgres -U yourname

# Create a database named: nextdb.
# If you change this, update config.js
CREATE DATABASE nextdb;

# Give your self privileges
GRANT ALL PRIVILEGES ON DATABASE nextdb TO yourname;

# List all of your databases
\list

# Connect to your newly created DB as a test
\connect nextdb

# Exit Postgres console
\q
```

I also use a GUI called [TablePlus](https://tableplus.io/) if you don't like command line.

## Setup: Run locally

In the root directory run these commands:

```sh
npm install
npm install -g sequelize-cli
sequelize db:migrate
npm run dev
```

Visit `localhost:8000` in a browser to start development locally. You will need postgres running.

## Deploy

Deploying with `now-cli` is as simple as

```sh
now

# after the deploy, alias to your domain, add "alias" to now.json first
now alias
```

Make sure you configure your alias for [zeit.world](https://zeit.world). Also make sure you add the secrets you need or delete the ones you aren't using from `now-secrets.json`.

## Secrets

You can update production secrets in `now-secrets.json` and `now.json`. You can add a secret to your Zeit deployment by typing

```sh
now secrets add production-username test
```

```sh
PrisBook:next-postgres2$[master !] now secrets add production-username test
> UPDATE AVAILABLE The latest version of Now CLI is 11.4.5
> Read more about how to update here: https://zeit.co/update-cli
> Changelog: https://github.com/zeit/now-cli/releases/tag/11.4.5
> Success! Secret production-username added (idkjs) [307ms]
PrisBook:next-postgres2$[master !] now secrets add production-password test
> UPDATE AVAILABLE The latest version of Now CLI is 11.4.5
> Read more about how to update here: https://zeit.co/update-cli
> Changelog: https://github.com/zeit/now-cli/releases/tag/11.4.5
> Success! Secret production-password added (idkjs) [292ms]
PrisBook:next-postgres2$[master !] now secrets add production-database nextdb
> UPDATE AVAILABLE The latest version of Now CLI is 11.4.5
> Read more about how to update here: https://zeit.co/update-cli
> Changelog: https://github.com/zeit/now-cli/releases/tag/11.4.5
> Success! Secret production-database added (idkjs) [295ms]
PrisBook:next-postgres2$[master !] now secrets add production-host 138.197.11.92
> UPDATE AVAILABLE The latest version of Now CLI is 11.4.5
> Read more about how to update here: https://zeit.co/update-cli
> Changelog: https://github.com/zeit/now-cli/releases/tag/11.4.5
> Success! Secret production-host added (idkjs) [295ms]
PrisBook:next-postgres2$[master !] now secrets add production-port 5432
> UPDATE AVAILABLE The latest version of Now CLI is 11.4.5
> Read more about how to update here: https://zeit.co/update-cli
> Changelog: https://github.com/zeit/now-cli/releases/tag/11.4.5
> Success! Secret production-port added (idkjs) [298ms]
PrisBook:next-postgres2$[master !] now secrets add production-secret test
> UPDATE AVAILABLE The latest version of Now CLI is 11.4.5
> Read more about how to update here: https://zeit.co/update-cli
> Changelog: https://github.com/zeit/now-cli/releases/tag/11.4.5
> Success! Secret production-secret added (idkjs) [295ms]
```

## Questions?

Feel free to slang any feels to [@wwwjim](https://twitter.com/wwwjim).
