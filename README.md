# World of Tanks Data
An easy-to-use collection of all data from [World of Tanks Miniatures Game](https://www.gf9games.com/worldoftanks/) by [Gale Force Nine](https://www.gf9games.com/). The idea, content, and structure are shamelessly copied from the amazing [X-Wing Data 2](https://github.com/guidokessels/xwing-data2) repository and adapted for World of Tanks Minatures Game.

## WOTS IDs
Every tank, upgrade, etc. has a `wots` field that contains an unique ID.

IDs are based on [X-Wing Squadron Specification (or `xws`)](https://github.com/elistevens/wots-spec/), and using the following steps:

1. Take the English-language name as printed on the card
2. Lowercase the name
3. Convert non-ASCII characters to closest ASCII equivalent (to remove umlauts, etc.)
4. Remove non-alphanumeric characters
5. Check for collisions, and add expansion suffixes until there is no more collision

wots ids have to be unique per type (pilot/upgrade/condition/etc) and do not collide with ids of other types. So there can be a `hansolo` _tanks_ and a `hansolo` _upgrade_, but there cannot be two upgrades with the `hansolo` wots id (regardless of the slot of those upgrades). One of those cards would get the `-slotname` suffix (for example: `hansolo-gunner`).

This project uses [SemVer](http://semver.org/). Given a `MAJOR.MINOR.PATCH` version number, we will increment the:

- `MAJOR` version when existing content is changed in such a way that it can break consumers of the data
- `MINOR` version when new content is added in a backwards-compatible manner, or existing content is changed in a backwards-compatible manner
- `PATCH` version when fixing mistakes in existing content

## History

See the [Releases tab](https://github.com/urbknu/wot-data/releases) in Github.

---

World of Tanks and all related properties, images and text are owned by Gale Force Nine and/or Wargaming.net
