# stylelint-at-rule-import-path

[![Build Status](https://travis-ci.org/timothyneiljohnson/stylelint-at-rule-import-path.svg)](https://travis-ci.org/timothyneiljohnson/stylelint-at-rule-import-path)

A custom [stylelint](https://github.com/stylelint/stylelint) rule to catch usage of `@import` statement underscores or filename extensions.

This rule will cause stylelint to error or warn you whenever `@import` include leading filenames underscores or filename extensions. It will also do it if there are some plain CSS imports (they are [claimed to be bad for performance](https://gtmetrix.com/avoid-css-import.html)).

## Installation

```
npm install stylelint-at-rule-import-path
```

This plugin is compatible with v5.0.1+.

## Details

There are 3 options: `allowUnderscore` (true|false), `allowExtension` (true|false), `allowCssImports` (true|false).

With default (no options specified):
```css
@import('_variables); /* Not OK */
@import('variables); /* OK */

@import('path/_variables); /* Not OK */
@import('path/variables); /* OK */

@import('variables.scss); /* Not OK */
@import('variables); /* OK */

@import('variables.css); /* Not OK */
@import('variables); /* OK */
```

With `allowUnderscore: true`:
```css
@import('_variables); /* OK */
@import('path/_variables); /* OK */
```

With `allowExtension: true`:
```css
@import('variables.scss); /* OK */
```

With `allowCssImports: false`:
```css
@import('variables.css); /* Not OK */
@import('variables); /* OK */
```

## Usage

Add `"stylelint-at-rule-import-path"` to your stylelint config `plugins` array, then add `at-rule-import-path` to your rules, set to your preferred options.

As follows:

```js
{
  "plugins": [
    "stylelint-at-rule-import-path"
  ],
  "rules": {
    "at-rule-import-path": [true, {
      allowUnderscore: [true|false],
      allowExtension: [true|false],
      allowCssImports: [true|false]
    }]
  }
};
```
