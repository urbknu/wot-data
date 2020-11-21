# X-Wing Data 2

An easy-to-use collection of all data from [X-Wing: The Miniatures Game (Second Edition)](https://www.fantasyflightgames.com/en/products/x-wing-second-edition/) by [Fantasy Flight Games](http://fantasyflightgames.com/).

If you're looking for data and images of X-Wing First Edition, you can find that here: [xwing-data](https://github.com/guidokessels/xwing-data).

## wots ids

Every ship, pilot, upgrade, etc. has a `wots` field that contains an unique id. These ids are used in the [X-Wing Squadron Specification (or `wots`)](https://github.com/elistevens/wots-spec/).

New wots ids are generated using the following steps:

1. Take the English-language name as printed on the card
2. Lowercase the name
3. Convert non-ASCII characters to closest ASCII equivalent (to remove umlauts, etc.)
4. Remove non-alphanumeric characters
5. Check for collisions, and add expansion suffixes until there is no more collision

Expansion suffixes per type:
Pilots: `pilotname-shipname-factionname-productsku`
Upgrades: `upgradename-slotname-productsku`
Conditions: `conditionname-productsku`

wots ids have to be unique per type (pilot/upgrade/condition/etc) and do not collide with ids of other types. So there can be a `hansolo` _pilot_ and a `hansolo` _upgrade_, but there cannot be two upgrades with the `hansolo` wots id (regardless of the slot of those upgrades). One of those cards would get the `-slotname` suffix (for example: `hansolo-gunner`).

## Scripts

There are a few scripts that make it easier to work on the data.

You can run these scripts using `npm` or `yarn`. For example:

- `npm run hyperspace`
- `yarn run hyperspace`

### Scripts to update data

| Script                | Description                                                                                                         |
| --------------------- | ------------------------------------------------------------------------------------------------------------------- |
| `yarn run hyperspace` | Syncs the `hyperspace` status of all cards with the gf9 squadbuilder                                                |
| `yarn run gf9scrape`  | Syncs all data with the gf9 squadbuilder (and alerts on missing cards)                                              |
| `yarn run gf92wots`    | Generates the [`data/gf9-wots.json`](https://github.com/guidokessels/xwing-data2/blob/master/data/gf9-wots.json) file |

### Scripts to work with the repository

| Script                          | Description                                                                                                                                                 |
| ------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `yarn run format`               | Format all `.json` files in the `data` folder using [Prettier](https://prettier.io/)                                                                        |
| `yarn run changelog A...B`      | Generate a changelog between commits `A` and `B`, to be used in the release description on GitHub.<br />Example usage: `yarn run changelog 1.24.0...1.25.0` |
| `yarn run validate:json`        | Validate that all `.json` files contain valid JSON                                                                                                          |
| `yarn run validate:tests`       | Run all unit tests                                                                                                                                          |
| `yarn run validate:tests:watch` | Run all unit tests in watch mode                                                                                                                            |

## Creating a release

Go through these steps to create a new release:

1. Make sure to run `yarn run gf92wots` to verify that `data/gf9-wots.json` has been updated
1. Bump the version number in `package.json` and `data/manifest.json` according to the [Versioning](#Versioning) rules listed below
1. Push the `package.json` and `data/manifest.json` changes to GitHub and/or merge them to the `master` branch
1. [Create a new release](https://github.com/guidokessels/xwing-data2/releases/new) on GitHub and use the following:
   - `Tag version`: The tag you just created
   - `Target`: `master` branch
   - `Release title`: The version number
   - `Describe this release`: The output of the `yarn run changelog PREVIOUS_VERSION...HEAD` command (replace `PREVIOUS_VERSION` with the [latest available tag](https://github.com/guidokessels/xwing-data2/tags))
1. All done! :tada:

## Versioning

This project uses [SemVer](http://semver.org/). Given a `MAJOR.MINOR.PATCH` version number, we will increment the:

- `MAJOR` version when existing content is changed in such a way that it can break consumers of the data
- `MINOR` version when new content is added in a backwards-compatible manner, or existing content is changed in a backwards-compatible manner
- `PATCH` version when fixing mistakes in existing content

## History

See the [Releases tab](https://github.com/guidokessels/xwing-data2/releases) in Github.

## License

[MIT](http://guidokessels.mit-license.org/)

---

Star Wars, X-Wing: The Miniatures Game and all related properties, images and text are owned by Fantasy Flight Games, Lucasfilm Ltd., and/or Disney.