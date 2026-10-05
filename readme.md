# Movie Review Chain

A small Cosmos SDK blockchain where movies and reviews live on chain. Anyone can add a movie with its title, description and year, and other people can post reviews with a rating. Only the account that created a movie or review can edit or delete it.

The project was scaffolded with Ignite CLI. All the chain logic is in the `movie` module, and there's a generated Vue web app for browsing and submitting entries.

## Tech stack

- Cosmos SDK 0.45 with Tendermint
- Ignite CLI for scaffolding and local development
- Go 1.18
- Vue 3 and Vite for the web app

## Running the chain

Install [Ignite CLI](https://docs.ignite.com), then from the repo root:

```bash
ignite chain serve
```

This installs dependencies, builds the `movied` binary, creates a local test chain and starts it. The accounts in `config.yml` get funded at genesis: `alice` is the validator and `bob` runs the faucet.

## Using it from the command line

```bash
# add a movie
movied tx movie create-movie "Arrival" "Linguist meets aliens" 2016 --from alice

# review it (movie id, rating, text)
movied tx movie create-review 0 5 "Smart and moving" --from bob

# read things back
movied query movie list-movie
movied query movie show-review 0
```

Movies can be changed with `update-movie` and `delete-movie`, and reviews with `update-review` and `delete-review`.

## Web app

```bash
cd vue
npm install
npm run dev
```

The app talks to the local chain started by `ignite chain serve`.

## Project structure

```text
x/movie/      The movie module: keeper, messages, queries and CLI
proto/movie/  Protobuf definitions for movies, reviews and the module's API
app/          Chain setup
cmd/movied/   The node binary
vue/          Generated web app
```
