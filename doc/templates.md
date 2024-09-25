# Flake Templates

We provide four templates, depending on your needs:

## Available templates

{#both}
### Both platforms

NixOS, nix-darwin, [home-manager] configuration combined, with common modules.

```bash
nix --accept-flake-config run github:juspay/omnix --
  init -o ~/nix-config github:srid/nixos-flake#both
```

{#nixos}
### NixOS only

NixOS configuration only, with [home-manager]

```sh
nix --accept-flake-config run github:juspay/omnix --
  init -o ~/nix-config github:srid/nixos-flake#linux
```

{#macos}
### macOS only

nix-darwin configuration only, with [home-manager]

```sh
nix --accept-flake-config run github:juspay/omnix --
  init -o ~/nix-config github:srid/nixos-flake#macos
```

{#home}
### Home only

[home-manager] configuration only (useful if you use other Linux distros or do not have admin access to the machine)

```bash
nix --accept-flake-config run github:juspay/omnix --
  init -o ~/nix-config github:srid/nixos-flake#home
```

## After initializing the template

1. Open `flake.nix` and change the user (from `john`) and hostname (from `example1`)[^intel]
    - Run `echo $USER` and `hostname -s` to determine the new values.
1. Then run `nix run .#activate` (`nix run .#activate $USER` if you are using the 4th template, "Home only") to activate the configuration.
    - on macOS, if you get an error about `/etc/nix/nix.conf`, run:
      ```sh
      sudo mv /etc/nix/nix.conf /etc/nix/nix.conf.before-nix-darwin
      nix --extra-experimental-features "nix-command flakes" run .#activate
      ```
    - on macOS, if you had used Determinate Systems nix-installer, you may want to [uninstall that Nix](https://github.com/LnL7/nix-darwin/issues/931#issuecomment-2075596824), such that we use the one provided by nix-darwin,
      ```sh
      sudo -i nix-env --uninstall nix
      ```

[^intel]: If you are on an Intel Mac, also change `nixpkgs.hostPlatform` accordingly.

[home-manager]: https://github.com/nix-community/home-manager
