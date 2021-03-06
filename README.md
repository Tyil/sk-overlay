[![Build Status](https://travis-ci.org/scriptkitties/overlay.svg?branch=master)](https://travis-ci.org/scriptkitties/overlay)

# Installation
## Using layman
Installation using layman is pretty straightforward:

```
layman -a scriptkitties
emerge --sync
```

## Manual installation
Add this to `/etc/portage/repos.conf/sk-overlay.conf`.

```
[sk-overlay]
location   = /usr/local/overlay/sk-overlay
sync-type  = git
sync-uri   = https://github.com/scriptkitties/overlay.git
auto-sync  = yes
```

`/usr/local/overlay` doesn't exist by default so create it if needed.
```
[ ! -d /usr/local/overlay ] && mkdir -p /usr/local/overlay
```

Finally you can update portage.
```
emerge --sync
```

# Usage
Like all overlays, there are various methods of checking what the overlay
contains. You could read through the git page, or you could go with the lazy
alternative which uses `app-portage/eix`. First make sure your eix cache is
up-to-date.
```
eix-update
```

Then to search all ebuilds contained in this overlay, you can issue the
following command:
```
eix --in-overlay sk-overlay
```

Too install from one of the ebuilds in sk-overlay, the installation process
is exactly the same as all normal gentoo packages. For instance, if you want to
install `void-sources-bin`, you could simply:
```
emerge -a void-sources-bin
```

# Issues
If you find any issues, such as repackaged software being out of date, you can
either [open an issue][new-issue] or join the IRC channel and hit up the
maintainer of the package. We reside on `irc.darenet.org` in `#scriptkitties`.

# Contributing
In order to ensure the quality of our overlay, we require a certain way to work
in order to get your ebuilds accepted.

- Fork the overlay
- Add/update/remove the ebuilds you want
- Run `repoman` to ensure it meets the Gentoo quality standards
  - If required, fix all issues reported by repoman
- Create a commit using `repoman ci`
  - Describe what you changed, in imperative form
  - Make sure the first line of the message is no more than 79 characters
  - Additional comments may be provided in the body of the commit message
- Open a PR on the upstream overlay repository

The PR will be checked using [Travis CI][travis] to make sure `repoman` has no
further complaints on the overlay. Once the checks have passed, one of our
maintainers will merge the commit for you. If it takes too long, drop by on
IRC and ask for someone to look at it.

## Requirements
There are some requirements your ebuild should adhere to in order to be
considered for our overlay.

- Your commits have to be signed.
- The software installed by the ebuild **must** be released under a free license
  (any license in `@FREE`).


[new-issue]: https://github.com/scriptkitties/overlay/issues/new
[darenet]: https://www.darenet.org
[travis]: https://travis-ci.org
