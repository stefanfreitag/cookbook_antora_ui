# cookbook_antora_ui

## Prerequisites

To preview and bundle the UI, you need the following software on your computer:

* `git`
* `node` and `npm`
* `gulp`

## git

First, make sure you have git installed.

```shell
git --version
```

## Node.js

Next, make sure that you have Node.js installed (which also provides npm).

```shell
node --version
```


## Gulp CLI

You'll need the Gulp command-line interface (CLI) to run the build.
The Gulp CLI package provides the `gulp` command which, in turn, executes the version of Gulp declared by the project.

You can install the Gulp CLI globally (which resolves to a location in your user directory if you're using nvm) using the following command:

```shell
npm install -g gulp-cli
```

Verify the Gulp CLI is installed and on your PATH by running:

```shell
 gulp --version
```

## Preview the UI

The  UI project is configured to preview offline.
The files in the [.path]_preview-src/_ folder provide the sample content that allow you to see the UI in action.
In this folder, you'll primarily find pages written in AsciiDoc.
These pages provide a representative sample and kitchen sink of content from the real site.

To build the UI and preview it in a local web server, run the `preview` command:

```shell
gulp preview
```

You'll see a URL listed in the output of this command:

```plaintext
[12:00:00] Starting server...
[12:00:00] Server started http://localhost:5252
[12:00:00] Running server
```

Navigate to this URL to preview the site locally.

While this command is running, any changes you make to the source files will be instantly reflected in the browser.
This works by monitoring the project for changes, running the `preview:build` task if a change is detected, and sending the updates to the browser.

Press kbd:[Ctrl+C] to stop the preview server and end the continuous build.

## Package for Use with Antora

If you need to package the UI so you can use it to generate the documentation site locally, run the following command:

```shell
gulp bundle
```

If any errors are reported by lint, you'll need to fix them.

When the command completes successfully, the UI bundle will be available at [.path]_build/ui-bundle.zip_.
You can point Antora at this bundle using the `--ui-bundle-url` command-line option.

If you have the preview running, and you want to bundle without causing the preview to be clobbered, use:

```shell
gulp bundle:pack
```

The UI bundle will again be available at [.path]_build/ui-bundle.zip_.

### Source Maps

The build consolidates all the CSS and client-side JavaScript into combined files, [.path]_site.css_ and [.path]_site.js_, respectively, in order to reduce the size of the bundle.
{url-source-maps}[Source maps] correlate these combined files with their original sources.

This "`source mapping`" is accomplished by generating additional map files that make this association.
These map files sit adjacent to the combined files in the build folder.
The mapping they provide allows the debugger to present the original source rather than the obfuscated file, an essential tool for debugging.

In preview mode, source maps are enabled automatically, so there's nothing you have to do to make use of them.
If you need to include source maps in the bundle, you can do so by setting the `SOURCEMAPS` environment variable to `true` when you run the bundle command:

```shell
SOURCEMAPS=true gulp bundle
```

In this case, the bundle will include the source maps, which can be used for debugging your production site.
