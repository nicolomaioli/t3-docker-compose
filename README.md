# Create T3 App - Docker Compose example

This is a [T3 Stack](https://create.t3.gg/) project bootstrapped with
`create-t3-app`.

This example shows how to:

- Spin up a `mysql` while running the application with `npm run dev`;
- Sping up a production build of the application alongside a `mysql` database
  in a single `docker compose` stack, running locally.

The development workflow looks like:

```sh
npm install

# spin up the mysql database
npm run compose:up

# push db changes
npm run prisma:push

# develop the application locally taking advantage of HMR etc.
npm run dev

# kill the stack
npm run compose:down
```

To check the production build, either locally or in a CI environment, run:

```sh
# spin up a docker-compose stack with both the database and a prod build of the
# application. Note that this will share the same volume as spinning up the db
# only, devising a strategy to run migrations or push changes is your
# responsibility. Also note that this will build the application every time.
npm run compose:local:up

# visit the application at localhost:8080

# kill the stack
npm run compose:local:down
```
