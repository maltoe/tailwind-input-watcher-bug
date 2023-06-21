# Watching input files breaks when listing directories in `content`

This minimal working example demonstrates a bug present in tailwindcss v3.2.2.

## Description

When a pattern with a directory is listed in the `content` option, the watching of input files ceases to function, **unless** the input files reside within the same directory.

For instance, in newly generated Phoenix v1.7.5 projects, the input file is `assets/css/app.css` and the content is set to `assets/js/**/*js` and `lib/my_app_web/...<path to heex files>`. Changes to the `app.css` **do not cause** the watcher to trigger.

## To reproduce this bug

```
npx tailwindcss --config tailwind-good.config.js --input main.css --output dist.css --watch

# ... make edit to main.css
# ... observe recompilation
```

```
npx tailwindcss --config tailwind-bad.config.js --input main.css --output dist.css --watch

# ... make edit to main.css
# ... observe no recompilation
```

Expected behaviour for both cases: Asset is recompiled when `main`.css is changed.

## To reproduce this repository

Just for reference:

```
- `npx tailwindcss init`
- Drop standard import directorives in `main.css`
- Create an empty directory called `some-dir`
```

