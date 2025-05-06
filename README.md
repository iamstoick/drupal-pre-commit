##  I love coffee!
https://buymeacoffee.com/stoickthevast

##  Want to help?
Looking for a maintainer. Please create an issue if you're interested.

Git Pre-Commit Hook Setup:
-------------------------

[![Gitter](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/geraldvillorente/drupal-pre-commit?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

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
* You must commit from project root or adjust relative paths to vendor/bin/.
* TwigCS doesn’t support auto-fix yet, but it gives detailed violations.
* Consider adding .twigcs.yml config for custom rules if needed.

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

## Bypassing the pre-commit hook
If you're really sure that it is ok to commit the changes without resolving the coding standard problem detected by the script, you can skip or bypass the validation by using <strong>--no-verify</strong>

```
$ git commit -am "#1452 Commit message | Bypassing validation process" --no-verify
```


-----------------------------------------------------------------------------------------------------------------------
-----------------------------------------------------------------------------------------------------------------------

This is optional and not required by pre-commit.

Install <strong>Esprima</strong> as JS validator.

To install Esprima:

`sudo npm -g install esprima`

To manually run Esprima from commandline interface.

1. <strong>esvalidate foo.js</strong> - For single file
2. <strong>esvalidate foo.js bar.js</strong> - For multiple files


For Geany IDE user:
-------------------
1. Open any JavaScript file (*.js)
2. Go to menu Build > Set Build Commands
3. At JavaScript Commands, click on the first "Set menu item label" button, type in "Esprima"
4. For the command, type in <strong>esvalidate %f</strong>
5. For the working directory, type in <strong>%d</strong>


To use it (e.g., in <strong>Geany IDE</strong>):
------------------
1. Build > Esprima

<a rel="license" href="http://creativecommons.org/licenses/by-nc/3.0/deed.en_US"><img alt="Creative Commons License" style="border-width:0" src="http://i.creativecommons.org/l/by-nc/3.0/88x31.png" /></a><br /><span xmlns:dct="http://purl.org/dc/terms/" property="dct:title">Drupal Pre Commit Filter</span> by <span xmlns:cc="http://creativecommons.org/ns#" property="cc:attributionName">Gerald Villorente</span> is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-nc/3.0/deed.en_US">Creative Commons Attribution-NonCommercial 3.0 Unported License</a>.<br />Based on a work at <a xmlns:dct="http://purl.org/dc/terms/" href="http://www.niden.net/2011/11/git-pre-commit-another-check-to-ensure.html" rel="dct:source">http://www.niden.net/2011/11/git-pre-commit-another-check-to-ensure.html</a>.

KNOWN ISSUES:
-------------

Please see this [issue](https://github.com/geraldvillorente/drupal-pre-commit/issues/10).

This `drupal-pre-commit` is only compatible with PHP_CodeSniffer 1.x. If you are using version 2.x you need to downgrade to stable version 1.5.6.

Steps to downgrade:
```
1. sudo pear uninstall PHP_CodeSniffer
2. sudo pear install PHP_CodeSniffer-1.5.6
```

NOTE:
-----

Any any case that the pre-commit is jumping to Step #3, you have to update your precommit `$LIST` variable to remove `\#`. So from
```
LIST=$( git status | grep -e '\#.*\(modified\|added\|new file\)' | grep -v '\#.*\(features\|contribs\|devel\)' )
```
to
```
LIST=$( git status | grep -e '.*\(modified\|added\|new file\)' | grep -v '.*\(features\|contribs\|devel\)' )
```

DISCUSSION CHANNEL:
-------------------
[https://gitter.im/geraldvillorente/drupal-pre-commit](https://gitter.im/geraldvillorente/drupal-pre-commit)
