# Tach self-host

Tach records how an organization's people use AI agents: which tools and models
ran, how many tokens they used and what that usage is estimated to cost. It
records counts and identifiers only, never prompts, responses or tool inputs
and outputs. This repository publishes the signed package that installs Tach for
one organization on one Linux VM that your IT team runs. It holds release files
only, no source code.

- Documentation: <https://tach-site.pages.dev/tools/tach/>
- Install guide: <https://tach-site.pages.dev/tools/tach/docs/install/prepare/>
- Releases: <https://github.com/r90group/tach-selfhost/releases>

## Release key

Public packages are signed with this minisign key. Its key ID is
`3ED2D71C174A84F7`. The install guide prints the same key; compare the two
before you trust either.

This public release key was established on 28 October 2026. Private
prereleases through 0.2.5 used key ID `4FF01EA23537AE88`; keep their original
key when verifying those packages.

```text
untrusted comment: minisign public key 3ED2D71C174A84F7
RWT3hEoXHNfSPouklRIs0r5zm+gbI7wA0/2esk8C164WwFi7bPqDhEeo
```

## Verify a download

Each release has the package `tach-selfhost-VERSION.tar.gz` and its hash file
`tach-selfhost-VERSION.tar.gz.sha256`. Replace `VERSION` with the release
version, such as `0.3.0`. On Ubuntu:

```sh
cat > trusted-release.pub <<'EOF'
untrusted comment: minisign public key 3ED2D71C174A84F7
RWT3hEoXHNfSPouklRIs0r5zm+gbI7wA0/2esk8C164WwFi7bPqDhEeo
EOF
curl --fail --location --remote-name https://github.com/r90group/tach-selfhost/releases/download/vVERSION/tach-selfhost-VERSION.tar.gz
curl --fail --location --remote-name https://github.com/r90group/tach-selfhost/releases/download/vVERSION/tach-selfhost-VERSION.tar.gz.sha256
sha256sum --check tach-selfhost-VERSION.tar.gz.sha256
sudo apt-get update
sudo apt-get install -y minisign
mkdir tach-package-VERSION
tar -xzf tach-selfhost-VERSION.tar.gz -C tach-package-VERSION --strip-components=1
cd tach-package-VERSION
minisign -Vm SHA256SUMS -p ../trusted-release.pub && sha256sum --check SHA256SUMS
```

`sha256sum` must print `OK` for every file, and `minisign` must report a good
signature. The hash only catches a damaged download; the signature proves the
package is genuine. Never verify with the `release.pub` file inside a package or
the `trusted-release.pub` file attached to a release: a key that comes with a
download cannot prove that download. Then follow the install guide.

## Report a problem

Email <hello@r90group.com>. Never send keys, passwords or sign-in codes.

## License

See LICENSE.
