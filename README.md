# dokku-builder-nix

This is a plugin for [dokku][] that gives you the option of using [Nix][] to
build your app images, instead of the default Herokuish or Dockerfile builders.

[dokku]: http://dokku.viewdocs.io/dokku/
[Nix]: https://nixos.org/

## Installation

```sh
# dokku 0.23.2+
$ dokku plugin:install https://github.com/jameysharp/dokku-builder-nix.git
```

(As of this writing, the `builder-detect` trigger that this plugin relies on is
not yet in a released version of Dokku. See dokku/dokku#4379 for the current
status.)

## Usage

Create a `docker.nix` at the root of your app's source tree. The result of
running `nix-build` on that must be an executable which streams output
compatible with `docker load` to stdout. The Nixpkgs [dockerTools][]
`streamLayeredImage` function is the recommended way to do this: set
`config.Cmd` to a program which will listen for incoming HTTP connections on
`$PORT`.

[dockerTools]: https://nixos.org/manual/nixpkgs/stable/#sec-pkgs-dockerTools

## Motivation

See my blog post, [Quickly building minimal Docker containers with Nix][blog],
for the rationale behind this project.

[blog]: https://jamey.thesharps.us/2021/02/03/docker-containers-nix/

## License

This plugin is derived from dokku's builder-cnb, and released under the same
MIT license as Dokku itself. See the file [LICENSE](LICENSE).
