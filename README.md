# CS:GO Community Server Materials Downloader

`CSMD` downloads community server's files based on a colsole log of file requests. It is created for Linux, but can be used on macOS or Windows if needed.

## Rationale

When one chooses a community server in a server list, the client basically executes `connect <ip:port>`, thus establishing communication and requesting any additional files that are missing from the client. For some unknown reason, a reason only Valve employee can know, Linux client refuses to download any content from FastDL type of servers. It has been like that for a very long time and the problem [has been reported](https://github.com/ValveSoftware/csgo-osx-linux/issues/11) to Vavle Sep 23, 2014. Since the issue remained unsolved, I decided to create at least some workaround - this script.

## Installation

Since the script must not be run as root (as it will lock the downloaded files under root), execute this in a terminal exactly as written out as a regular user (i.e. not root)(this assumes `sudo` is configured correctly):

```
sudo curl -o /usr/local/bin/csgo-csmd https://raw.githubusercontent.com/light2yellow/csgo-csmd/master/csgo-csmd
sudo chown $USER:$USER /usr/local/bin/csgo-csmd
chmod +x /usr/local/bin/csgo-csmd
```

## Usage

1. Find a community server that your client refuses to connect to ("Downloading map <mapname> 0 % / 0 bytes").
2. Open CS:GO console (press `~` A.K.A. tilde, one has to have `-console` in the [game launch options](https://steamcommunity.com/sharedfiles/filedetails/?id=379782151)).
3. Type `disconnect` and press `Enter`.
4. Type `condump` and press `Enter`.
5. Open a terminal (the one with a shell session) and run `csgo-csmd`.
6. If the command output says "Success!" at the end, you might want to copy the `connect <ip:port>` on the very last line in order to quickly connect back to the server (use in-game console to execute the copied command).

### Command-line arguments

See `csgo-csmd --help`.

* `--csgo-path` - path to CS:GO folder. By default `.local/share/Steam/steamapps/common/Counter-Strike Global Offensive/csgo` is used.
* `--condump` - console dump, generated in step 4 above. Must have `condumpXXX.txt` syntax where `X` is a `0-9` digit.

## Bugs and feature requests

Open new tickets through [GitHub Issues](https://github.com/light2yellow/csgo-csmd/issues). Please take time to describe the problem and copy the logs the script produces.

## Caveats

`CSMD`:
  * doesn't know how to decompress anything except bzip2
  * doesn't talk HTTPS (only HTTP)

If any of the above makes your life worse, open a new issue.