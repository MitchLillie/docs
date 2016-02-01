<!--
title: 15 - Using tags
featured: true
-->

# Using dist-tags

Tags are a supplement to [semver](http://semver.org/) (e.g., v0.12) for
organizing and labeling different versions of packages. In addition to being
more human-readable, tags allow publishers to distribute their packages more
effectively.

## Adding tags

To add a tag to a specific version of your package, use
`npm dist-tag add <pkg>@<version> [<tag>]`. See
[the CLI docs](https://docs.npmjs.com/cli/dist-tag) for more information.

## Publishing with tags

By default, `npm publish` will tag your package with the `latest` tag. If you
use the `--tag` flag, you can specify another tag to use.

```
npm publish --tag <tag>
```

## Installing with tags

Like `npm publish`, `npm install <pkg>` will use the `latest` tag by default.
To override this behavior, use `npm install <pkg>@<tag>`.

```
npm install <package>@<tag>
```

## Example

Let's say you're the publisher of a module called `happycat`. Its purpose is
to brighten the lives of tired programmers by peppering output and log files
with cat gifs. You've just implemented a new feature in v0.2 to decorate every
`console` message with ASCII cats, but are wary of publishing such a big change
to all your users. You'll use the `ascii-console` tag to publish the new
feature to anyone on npm who wants it, and wait for their feedback before
rolling it into the main package. Make sure you've checked out the version with
the new feature, and then publish to npm with the new tag:

```
git checkout v0.2
npm publish --tag ascii-console
```

Now, users can access the new feature by specifying the tag to install:

```
npm install happycat@ascii-console
```

When you're satisfied that the ASCII feature is ready for all users, simply add
the `latest` tag to version 0.2:

```
npm dist-tag add happycat@0.2 latest
```

Now your users will get the ASCII feature by default:

```
npm install happycat
```

## Caveats

Because dist-tags share the same namespace with semver, avoid using any tag
names that may cause a conflict. The best practice is to avoid using tags
beginning with a number or the letter "v".
