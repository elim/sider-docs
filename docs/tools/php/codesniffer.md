---
id: codesniffer
title: PHP_CodeSniffer
sidebar_label: PHP_CodeSniffer
hide_title: true
---

# PHP_CodeSniffer

| Supported Version | Language  | Website                                      |
| ----------------- | --------- | -------------------------------------------- |
| 3.5.3             | PHP 7.4.2 | https://pear.php.net/package/PHP_CodeSniffer |

## Getting Started

To start using PHP_CodeSniffer, enable it in [Repository Settings](../../getting-started/repository-settings.md). To configure the coding standard you want to follow, add `sider.yml` in your repository and set the `standard` option:

```yaml
linter:
  code_sniffer:
    dir: app/
    options:
      standard: CakePHP
```

## Default Configuration

If you don't specify anything, Sider tries to detect the standard and target directory for your project automatically.
If it cannot find an appropriate standard, it assumes `PSR2` as its standard and analyzes all PHP files in your repository.

### Standard and Analysis Target

Sider tries to detect the most suitable standard and target directory for your project,
based on the framework your project is using.

The following standards are detected automatically:

- `CakePHP`
- `Symfony`

The auto-detection is based on file names and directory structure in your repository.
If this auto-detection fails, you can specify a standard in `sider.yml`.

## Configuration via `sider.yml`

An example setting for PHP_CodeSniffer under `code_sniffer`:

```yaml
linter:
  code_sniffer:
    dir: app/
    standard: phpcs.xml
    extensions: php,inc,lib
    encoding: utf-8
    ignore: app/Vendor
```

You can use several options to fine-tune PHP_CodeSniffer to your project:

| Name                                                                        | Type                | Default | Description                                             |
| --------------------------------------------------------------------------- | ------------------- | ------- | ------------------------------------------------------- |
| [`root_dir`](../../getting-started/custom-configuration.md#root_dir-option) | `string`            | -       | A root directory.                                       |
| [`version`](#version)                                                       | `string`, `integer` | `3`     | Declare PHP_CodeSniffer version explicitly.             |
| [`dir`](#dir)                                                               | `string`            | `.`     | Set targets to analyze.                                 |
| [`standard`](#standard)                                                     | `string`            | `PSR2`  | Set coding standard or your config file when analyzing. |
| [`extensions`](#extensions)                                                 | `string`            | `php`   | Set extensions to analyze.                              |
| [`encoding`](#encoding)                                                     | `string`            | -       | Set file encoding.                                      |
| [`ignore`](#ignore)                                                         | `string`            | -       | Excludes files or directories from analysis.            |

### `version`

This option controls which major version of PHP_CodeSniffer is used.
Sider has stopped supporting v2 of PHP_CodeSniffer. Therfore, if you set `2` in this option, Sider will execute v3.

### `dir`

This option controls directories Sider inspects. The default value is dependent on the frameworks PHP_CodeSniffer supports.
If you are not using any frameworks or are using a framework PHP_CodeSniffer does not support, `.` is used.

If you would like to exclude specific directories, you can specify them in a custom ruleset file.

### `standard`

This option controls a coding standard of your project. If you leave this value empty, Sider tries to detect the standard automatically.

`PSR2` is used when auto detection fails.

You can use the following third-party standards in addition to the standards which PHP_CodeSniffer supports natively:

- [Symfony](https://github.com/djoos/Symfony-coding-standard)
- [CakePHP](https://github.com/cakephp/cakephp-codesniffer)
- [WordPress](https://github.com/WordPress/WordPress-Coding-Standards)

If you want to see the actual standard lists, run the command [`phpcs -i`](https://github.com/squizlabs/PHP_CodeSniffer/wiki/Usage#printing-a-list-of-installed-coding-standards).
The following output is a standard list which Sider prepares.

```shell
$ phpcs -i
The installed coding standards are Zend, PSR12, MySource, Squiz, PSR2, PSR1, PEAR, CakePHP, Symfony, WordPress, WordPress-Extra, WordPress-Docs and WordPress-Core
```

You can also define your own standard, and enter the path to the config file here.

### `extensions`

This option controls a comma-separated list of extensions of files which Sider inspects.

### `encoding`

This option controls file encoding.

### `ignore`

A comma-separated list of patterns to ignore files and directories by.
