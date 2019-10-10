# @knowitsolutions/react-scripts

This package is a fork of [Create React App](https://github.com/facebookincubator/create-react-app) (specifically the
`react-scripts` package). It's intended to be used in conjuction with `create-react-app` like so:

```sh
yarn create react-app my-app --scripts-version=@knowitsolutions/react-scripts

# start your app development like you normally would with `create-react-app`
cd my-app
yarn start
```

The setup of this fork has been modeled after another react-scripts fork: [backpack-react-scripts](https://github.com/Skyscanner/backpack-react-scripts)

## What is different in our fork?

- [source-map-loader](https://github.com/webpack-contrib/source-map-loader) added to webpack configuration.
- Source maps enabled by default for dependecies.
- Allow more jest confiuration overrides: `setupTestFrameworkScriptFile`, `testMatch`.

## Releasing a new version of `@knowitsolutions/react-scripts`

1. To publish a new version of `@knowitsolutions/react-scripts`, run the following command:

   ```
   npm run publish prerelease
   ```

   - If you want to be extra careful, you can publish a prerelease by running this instead:

   ```
   npm run publish --canary
   ```

1. Update the [CHANGELOG.md](./CHANGELOG.md) with the new version, taking care to follow the format of previous releases.

## Keeping this fork updated

We wish to keep this fork updated with the upstream repo to benefit from the ongoing open source development
of `create-react-app`. To keep this fork up to date, please follow the steps below:

1. Ensure `master` is in sync with `upstream/master`:

   ```sh
   git checkout master
   git remote add upstream git@github.com:facebook/create-react-app.git
   git fetch upstream
   git reset --hard upstream/master
   git push --force-with-lease
   ```

1. Rebase `fork` on top of a **tagged release** on `master`:

   ```sh
   git checkout fork
   git rebase <commit>
   ```

   > **Note:** `<commit>` should be the SHA-1 of the latest upstream release - _not_ just the latest i.e. `upstream/master`

1. Pair with someone else to fix any conflicts and cross examine changes in upstream with changes in our fork.

   > This is the most time consuming part. Take care to make sure you are not regressing any functionality that we have added in our fork.

1. Re-name your local, rebased `fork` branch to something else and push it to origin. This will ensure it runs through CI and you can verify your changes.

   ```sh
   git branch -m <branch>
   git push origin <branch>
   ```

1. Finally, when we are confident that the rebase has been successful, re-name your branch back to `fork` and push it to origin:

   ```sh
   git branch -m fork
   git push --force-with-lease
   ```
