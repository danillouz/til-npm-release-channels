# TIL npm Release Channels
Today I learned about [npm](https://www.npmjs.com) release
channels.

# Why?
Stop breaking things for people using your package and have
a more sustainable way of addressing releases by creating
**release channels**.

> Using release channels acts as an additional security net
to catch mistakes of any kind and adopting good habits early
leaves you well prepared for overwhelming success that might
follow later.

With release channels, updates can be rolled out in a very
controlled manner and by means of an update cycle of your
own choosing. For instance, take the [Chrome Release Channels](https://www.chromium.org/getting-involved/dev-channel):

- Stable
	* Fully tested.
	* Best bet to avoid crashes and other issues.
	* Updated roughly every _two-three weeks_ for _minor_ releases, and every _6 weeks_ for _major_ releases.
- Beta
	* See what's next, with minimal risk.
	* Updated _every week_ roughly, with _major_ updates coming every _six weeks_, more than a _month before the Stable channel will get them_.
- Dev
	* See what's happening quickly.
	* Updated _once or twice weekly_ and it shows what's worked on right now.
	* There's no lag between major versions.
	* Subject to bugs, because it shows what's new as soon as possible.
- Canary
 	* Bleeding edge.
	* Released _daily_.
	* Has not been tested or used.
	* No guarantee that it will even run in some cases.
	* Reports crashes and usage statistics by default.

# npm Distribution Tags
Support for release channels can be accomplished by means of
[npm package distribution tags](https://docs.npmjs.com/cli/dist-tag),
or **dist-tags**. In fact, if you ever typed `npm i <package>`
before, you have _implicitly_ used this feature already,
because npm uses the `latest` dist-tag by default.

# Publish a package with a dist-tag
```
npm publish --tag=<the name of your dist-tag>
```

For example:

```
npm publish --tag=canary
```

# Install a package with a dist-tag
```
npm i <package>@<the name of your dist-tag>
```

For example, if the name of my package is `supereact`,
then the command will be:

```
npm i supereact@canary
```

# Move the latest dist-tag over to the highest version
```
npm dist-tag add <package>@<your latest version> latest
```

For example, if the name of my package is `supereact`,
and the highest version is `98.0.1`, then the command will
be:

```
npm dist-tag add supereact@98.0.1 latest
```

# Use dist-tags to release multiple feature branches
By using a [semver pre-release version](http://semver.org/#spec-item-9)
in combination with a dist-tag, it's possible to release
multiple feature branches at the same time. For example:

- Branch `master` with dist-tag `v1.0.0`
- Branch `feature/1` with dist-tag `v1.0.1-feature.1`
- Branch `feature/2` with dist-tag `v1.0.1-feature.2`

# Configuring the dist-tag in `package.json`
It's also possible to set the name of the dist-tag in your
`package.json` file by using the [publishConfig](https://docs.npmjs.com/files/package.json#publishconfig)
property. This way you can make sure the correct dist-tag is
always set when publishing:

```json
"publishConfig": {
  "tag": "canary"
}
```

This can be convenient when releasing feature branches.

# Tools
- [semantic-release](https://github.com/semantic-release/semantic-release)

# Additional Resources
- [Article with very long title](https://blog.greenkeeper.io/one-simple-trick-for-javascript-package-maintainers-to-avoid-breaking-their-user-s-software-and-to-6edf06dc5617)
- [npm publishConfig docs](https://docs.npmjs.com/files/package.json#publishconfig)
- [npm dist-tag CLI docs](https://docs.npmjs.com/cli/dist-tag)
- [Video tutorial](https://www.youtube.com/watch?v=FjVS1U1cdXM)
- [semver pre-release version](http://semver.org/#spec-item-9)
- [Chrome Release Channels](https://www.chromium.org/getting-involved/dev-channel)

# License
MIT © [Daniël Illouz](https://github.com/danillouz)
