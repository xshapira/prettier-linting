# Linting Configuration

## Quick Setup (ES2015/ES6)

The quick setup guide will configure your project to use [Prettier](https://github.com/prettier/prettier) with [ESLint](https://eslint.org/) and [Stylelint](https://stylelint.io/) for projects written in ES2015 and Sass.

1. If you don't already have a `package.json` file in your project, run the following command in your shell
    ```sh
    npm init -y
    ```
1. Install the following npm packages *globally* for your text editor extensions:
    ```sh
    npm install -g eslint stylelint prettier prettier-eslint prettier-stylelint
    ```
1. Install the following npm packages as *devDependencies* for your project:
    ```sh
    npm install --save-dev eslint stylelint prettier prettier-eslint prettier-stylelint eslint-config-prettier eslint-config-standard eslint-plugin-prettier eslint-plugin-standard eslint-plugin-promise eslint-plugin-import eslint-plugin-node stylelint-config-sass-guidelines
    ```
1. In your project's `package.json` file, add the following configuration to the bottom:
    ```json
    {
        "prettier": {
            "printWidth": 80,
            "tabWidth": 2,
            "useTabs": false,
            "semi": true,
            "singleQuote": true,
            "trailingComma": "none",
            "bracketSpacing": true,
            "jsxBracketSameLine": false,
            "parser": "babylon",
            "overrides": [
                {
                    "files": "*.json",
                    "options": { "parser": "json" }
                }
            ]
        },
        "eslintConfig": {
            "plugins": ["prettier"],
            "extends": ["standard", "prettier"],
            "rules": {
                "prettier/prettier": "error"
            }
        },
        "stylelint": {
            "extends": [
                "stylelint-config-sass-guidelines",
                "./node_modules/prettier-stylelint/config.js"
            ]
        }
    }
    ```

## Prettier for Code Formatting

[Prettier](https://github.com/prettier/prettier) takes your code and reprints it from scratch by taking the line length into account.

### Installation

For projects:

```sh
npm install --save-dev prettier
```

If you're using Prettier as an extension for text editors (i.e. VSCode), you should install Prettier as a global package along with the text editor specific extension. See [editor integration](https://github.com/prettier/prettier#editor-integration) for Prettier.

```sh
npm install -g prettier
```

## Prettier With ESLint

If you're using Prettier with [ESLint](https://eslint.org/), you'll need to install [prettier-eslint](https://github.com/prettier/prettier-eslint) as an npm package *globally* for you text editor integration via extensions and as a *devDependency* in your project. `prettier-eslint` formats your JavaScript using prettier followed by `eslint --fix`.

**Note: The following instructions assumes you have Prettier setup as mentioned previously.**

### Install NPM Packages

```sh
# install globally for text editor integration
npm install -g prettier-eslint

# install as project devDependency
npm install --save-dev prettier-eslint
```

### Extending the ESLint Config

To serve as a base for our ESLint configuration, you'll need to install the npm package `eslint-config-standard`. This can be installed manually via npm or through the CLI.

#### Adding eslint-config-standard via CLI

To add `eslint-config-standard` with the  CLI method, first navigate to the root of your project and execute the following command in your preferred shell.

```sh
eslint --init
```

ESLint's `eslint --init` command will walk you through a series of questions that will later download, install, and configure any necessary dependencies.

In the prompt, make the following selections to the `eslint --init` questions:

1. Select **Use a popular style guide**.
1. Select **Standard**.
1. Select **JSON**.

After executing `eslint --init`, a file named `.eslinrc.json` should have been created at the root level of your project.

`.eslintrc.json`

```json
{
    "extends": "standard"
}
```

#### Adding eslint-config-standard Manually

To install `eslint-config-standard` run the following command via npm:

```sh
npm install --save-dev eslint-config-standard eslint-plugin-standard eslint-plugin-promise eslint-plugin-import eslint-plugin-node
```

Create an ESLint configuration file as either `.eslintrc` or `.eslintrc.json` at the root of your project and add the following configuration.

`.eslintrc`

```json
{
    "extends": "standard"
}
```

### Disable Conflicting ESLint Rules

To avoid having rule conflicts with Prettier and ESLint, install [eslint-config-prettier](https://github.com/prettier/eslint-config-prettier).

```sh
npm install --save-dev eslint-config-prettier
```

Once you've installed the npm package `eslint-config-prettier`, you'll need to add `"prettier"` last in the `extend` property of the [ESLint configuration file](#eslint-configuration-file) to override any conflicting rules set by `eslint-config-standard`.

```json
{
    "extends": [
        "standard",
        "prettier"
    ]
}
```

### Prettier Plugin for ESLint

Installing [eslint-plugin-prettier](https://github.com/prettier/eslint-plugin-prettier) allows you to run Prettier as an ESLint rule and report differences.

```sh
npm install --save-dev eslint-plugin-prettier
```

The `eslint-plugin-prettier` ruleset configuration should be added as `"prettier"` to the `"plugins"` property of the [ESLint configuration file](#eslint-configuration-file). In addition, add `"prettier/prettier"` rules

`.eslintrc`

```json
{
    "plugins": ["prettier"],
    "extends": [
        "standard",
        "prettier"
    ],
    "rules": {
        "prettier/prettier": "error"
    }
}
```

### ESLint Configuration File

You can configure ESLint either by creating a `.eslintrc` file or by adding a `"eslintConig"` key in your `package.json` file.

`.eslintrc`:

```json
{
    "plugins": ["prettier"],
    "extends": ["standard", "prettier"],
    "rules": {
        "prettier/prettier": "error"
    }
}
```

`package.json`

```json
{
    "eslintConfig": {
        "plugins": ["prettier"],
        "extends": ["standard", "prettier"],
        "rules": {
            "prettier/prettier": "error"
        }
    }
}
```

## Prettier With Stylelint

If you're using Prettier with [Stylelint](https://stylelint.io/), you'll need to install [prettier-stylelint](https://github.com/hugomrdias/prettier-stylelint) as an npm package *globally* for you text editor integration via extensions and as a *devDependency* in your project. `prettier-stylelint` formats your JavaScript using prettier followed by `stylelint --fix`.

**Note: The following instructions assumes you have Prettier setup as mentioned previously.**

### Install prettier-stylelint

```sh
npm install --save-dev prettier-stylelint
```

### Extending the Stylelint Config

To serve as a base to our Stylint configuration, you'll need to install [stylelint-config-sass-guidelines](https://github.com/bjankord/stylelint-config-sass-guidelines) which is a Stylelint configuration based on the [sass-guidelin.es](https://sass-guidelin.es/).

```sh
npm install --save-dev stylelint-config-sass-guidelines
```

Once installed, `"stylelint-config-sass-guidelines"` should be set in the `"extend"` property of the [Stylelint configuration file](#stylelint-configuration-file) file.

`.stylelintrc`

```json
{
    "extend": [
        "stylelint-config-sass-guidelines"
    ]
}
```

### Disable Conflicting Stylelint Rules

To avoid having rule conflicts with Prettier and Styelint, add `"./node_modules/prettier-stylelint/config.js"` as the last item in the array of the `"extend"` property of the [Stylelint configuration file](#stylelint-configuration-file). Adding it as the last item ensures that it override any conflicting rules. This is made possible through the npm package `prettier-stylelint`.

```json
{
    "extends": [
        "stylelint-config-sass-guidelines",
        "./node_modules/prettier-stylelint/config.js"
    ]
}
```

### Stylint Configuration File

You can configure Stylelint either by creating a `.stylelintrc` file or by adding a `"eslintConig"` key in your `package.json` file.

`.stylelintrc`

```json
{
    "extends": [
        "stylelint-config-sass-guidelines",
        "./node_modules/prettier-stylelint/config.js"
    ]
}
```

`package.json`

```json
{
    "stylelint": {
        "extends": [
            "stylelint-config-sass-guidelines",
            "./node_modules/prettier-stylelint/config.js"
        ]
    }
}
```

## Prettier With Webpack

*In progress...*

## VSCode Integration
