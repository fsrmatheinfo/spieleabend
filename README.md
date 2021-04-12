# 🎲 spieleabend

Docker Compose bundle of collaborative, open source online games.

## Deployment

To start all game servers simply run:
```shell script
docker-compose up -d
```
The games run on [ports](#games) 40001 to 40013 on `localhost`.

## Games

- [Cards Against Humanity](https://github.com/emcniece/DockerYourXyzzy)
  <small> (Pretend You're Xyzzy) </small>:
  [`localhost:40001`](http://localhost:40001)
  BSD-2-Clause License
- [Pictionary](https://github.com/scribble-rs/scribble.rs):
  [`localhost:40002`](http://localhost:40002)
  BSD-3-Clause License
- [Battleship](https://github.com/manassarpatwar/WarVessels):
  [`localhost:40003`](http://localhost:40003)
  MIT License
- [Chess](https://github.com/Aveek-Saha/Online-Chess):
  [`localhost:40004`](http://localhost:40004)
  MIT License
- [Settlers of Catan](https://github.com/seansegal/tincisnotcatan):
  [`localhost:40005`](http://localhost:40005)
- [Cards Against Humanity](https://github.com/lattyware/massivedecks)
  <small> (Massive Decks) </small>:
  [`localhost:40006`](http://localhost:40006)
  AGPL-3.0 License
- [Spyfall](https://github.com/tannerkrewson/spyfall):
  [`localhost:40007`](http://localhost:40007)
  MIT License
- [Agar.io](https://github.com/huytd/agar.io-clone)
  <small> (Open Agar) </small>:
  [`localhost:40008`](http://localhost:40008)
  MIT License
- [Agar.io client](https://github.com/opcon/Cigar2)
  <small> (Cigar2) </small>:
  [`localhost:40009`](http://localhost:40009)
  ISC License
- [Agar.io server](https://github.com/opcon/OgarII)
  <small> (OgarII) </small>:
  [`localhost:40010`](http://localhost:40010)
  Apache License 2.0
- [Kung-Fu Chess](https://github.com/PetterS/realtimechess):
  [`localhost:40011`](http://localhost:40011)
  GPL-3.0 License
- [Codenames](https://github.com/jbowens/codenames):
  [`localhost:40012`](http://localhost:40012)
- [Werewolf](https://github.com/AlecM33/Werewolf):
  [`localhost:40013`](http://localhost:40013)

If you're missing your favorite game, and a web clone is available under an open license, we're happy to accept [whishes](https://github.com/fsrmatheinfo/spieleabend/issues) and [pull requests](https://github.com/fsrmatheinfo/spieleabend/pulls).

## Development

When a `Dockerfile` is changed, you might want to run:
```shell script
docker-compose build
```
This will rebuild images (but still use the build cache).

### Client-server apps
Games that run on multiple containers (e.g., client and server) should communicate inside a separate Docker network.
If that is no option, please verify that any backend address can be configured through `docker-compose.override.yml`.
This way the repo can be deployed on a public server.
