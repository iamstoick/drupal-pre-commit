[![Gitter](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/geraldvillorente/drupal-pre-commit?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

# Primo
This Git pre-commit hook ensures your Drupal codebase remains clean, standards-compliant, and production-ready by running a series of automated checks and fixes before each commit.

Use this hook to automatically catch and fix issues before code hits your repository, making your team’s codebase more consistent and easier to maintain.

##  Want To Support!
I love coffee, you can buy me here: https://buymeacoffee.com/stoickthevast

##  Want to help?
Looking for a maintainer. Please create an issue if you're interested.

Git Pre-Commit Hook Setup:
-------------------------

1. Rename pre-commit.sample to pre-commit. The file is located in {GitRootDir}/.git/hooks

2. Replace the content with the attached file.

3. Make sure that the file has an execute permission.

```
$ sudo chmod +x /path/to/.git/hooks/pre-commit
```

## Requirements:
-------------

You need to have a Code Sniffer installed before using this pre-commit script. To install.

```
& composer require --dev drupal/coder
& vendor/bin/phpcs --config-set installed_paths vendor/drupal/coder/coder_sniffer
$ vendor/bin/phpcs -i   # Confirm "Drupal" is listed

```

## Twig Linting Support?
--------------
In your Drupal project root, run:
```
$ composer require --dev friendsoftwig/twigcs
```

## CSS/SCSS Linting Support?
--------------
To enable CSS/SCSS linting support:
```
$ npm install --save-dev stylelint stylelint-config-standard
```

Create a `.stylelintrc.json` config file:
```
{
  "extends": "stylelint-config-standard"
}
```

## Notes
--------------
* You must commit from project root or adjust relative paths to `vendor/bin/`.
* TwigCS doesn’t support auto-fix yet, but it gives detailed violations.
* Consider adding `.twigcs.yml` config for custom rules if needed.

## ✅ What the Git Pre-commit Hook Supports
---------------

| Feature                     | Support Status      | Notes                                             |
|-----------------------------|---------------------|---------------------------------------------------|
| PHP syntax check            | ✅ Yes              | Uses `php -l`                                     |
| PHP code style (Drupal)     | ✅ Yes              | `phpcs` with auto-fix via `phpcbf`                |
| PHP debug statement check   | ✅ Yes              | Blocks on patterns like `dpm(`, `var_dump(`, etc. |
| JavaScript syntax & style   | ✅ Yes              | Uses `eslint --fix`                               |
| Twig linting                | ✅ Yes (no auto-fix)| Via `twigcs`                                      |
| Twig auto-fix               | ❌ Not supported    | Manual fix or IDE required                        |
| Auto-restaging fixed files  | ✅ Yes              | Uses `git add` after fixes                        |
| Composer-aware commands     | ✅ Yes              | Uses `vendor/bin` for local installs              |
| CSS/SCSS linting & auto-fix | ✅ Yes              | Uses stylelint                                    |

The <strong>pre-commit</strong> hook will only run when using <strong>git commit</strong>

If the commit contains any violations of the following type:

1. PHP syntax error
2. PHP coding standard
3. JavaScript coding standard
4. CSS coding standard

it will exit before the commit get indexed and will display the offending file(s).

it will display the line of code and the filename that contain bad code. The developer must resolve the problem first in order to stage the commit.

## 🚀 Pre-commit Hook Support Matrix
------------------

| Check Type             | Description                               | Status |
|------------------------|-------------------------------------------|--------|
| ✅ PHP Linting         | Checks for syntax errors                  | ✔️     |
| ✅ PHP Code Sniffer    | Drupal coding standards                   | ✔️     |
| 🔧 PHP Auto-fix        | Auto-corrects code style issues (phpcbf)  | ✔️     |
| 🚫 Debug Function Block| Prevents `var_dump()`, `dpm()`, etc.      | ✔️     |
| ✅ JS Linting          | ESLint validation                         | ✔️     |
| 🔧 JS Auto-fix         | Auto-fix JavaScript issues                | ✔️     |
| ✅ Twig Linting        | Enforces TwigCS rules                     | ✔️     |
| ⚠️ Twig Auto-fix       | Not supported (TwigCS is lint-only)       | 🚫     |
| ✅ CSS/SCSS Linting    | Stylelint rules enforcement               | ✔️     |
| 🔧 CSS Auto-fix        | Auto-fix for CSS/SCSS issues              | ✔️     |

> 💡 Tip: Be sure to install all dependencies (PHP, Composer, Node.js, ESLint, TwigCS, Stylelint) for this hook to work effectively.


## Bypassing the pre-commit hook
If you're really sure that it is ok to commit the changes without resolving the coding standard problem detected by the script, you can skip or bypass the validation by using `--no-verify`.

```
$ git commit -am "#1452 Commit message | Bypassing validation process" --no-verify
```

## Issues?
-----------
Please file an issue if you encounter any problem. Thanks for the support. 
