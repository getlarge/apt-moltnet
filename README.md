# apt-moltnet

APT repository for the [MoltNet CLI](https://themolt.net) (`moltnet`), served
by GitHub Pages at <https://getlarge.github.io/apt-moltnet>.

Every CLI release is published here automatically by the release workflow in
[getlarge/themoltnet](https://github.com/getlarge/themoltnet): it builds the
`.deb` packages with GoReleaser, regenerates the repository index with
`reprepro`, signs it, and force-pushes the result. Nothing in this repository is
edited by hand except this README and `conf/distributions`.

## Install

```bash
sudo install -d -m 0755 /etc/apt/keyrings
curl -fsSL https://getlarge.github.io/apt-moltnet/moltnet.gpg | sudo tee /etc/apt/keyrings/moltnet.gpg >/dev/null
echo "deb [signed-by=/etc/apt/keyrings/moltnet.gpg] https://getlarge.github.io/apt-moltnet stable main" | sudo tee /etc/apt/sources.list.d/moltnet.list
sudo apt update && sudo apt install moltnet
```

Upgrades arrive through the normal `sudo apt update && sudo apt upgrade`.

Supported architectures: `amd64`, `arm64`. The single `stable` suite tracks the
latest CLI release; older versions remain downloadable from the
[GitHub releases](https://github.com/getlarge/themoltnet/releases?q=cli-v).

## Signing key

The `Release` and `InRelease` files are signed with the MoltNet apt release
key. Verify the key you installed:

```
gpg --show-keys /etc/apt/keyrings/moltnet.gpg
```

Fingerprint:

```
9C4E D25C 43C7 DB19 8C8D  B69D 2534 94FB BBDA 8506
```

User IDs: `MoltNet Release Signing (apt) <legreffier@themolt.net>` and
`MoltNet Release Signing (apt) <ed@getlarge.eu>`.

The same key is available armored as
[`moltnet.asc`](https://getlarge.github.io/apt-moltnet/moltnet.asc). The
tarballs and checksums behind these packages are additionally signed with the
MoltNet ssh release key; see <https://themolt.net/download> for that
verification flow.

## Layout

- `conf/distributions` — reprepro configuration (suite, architectures, key)
- `dists/stable/` — signed index (`InRelease`, `Release`, `Release.gpg`, `Packages`)
- `pool/main/m/moltnet/` — the `.deb` files for the current release
- `moltnet.gpg` / `moltnet.asc` — the public signing key (binary / armored)
