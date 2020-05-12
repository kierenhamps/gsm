# Game Server Managers

Container version of Linux Game Server Managers for dedicated game hosting.

[linux GSM](https://docs.linuxgsm.com/) with tested support for:
[Stationeers](https://stationeers-wiki.com/Dedicated_Server_Guide)

## Building

To build use the following command:

```
docker build -t gsm:latest .
```

The ENTRYPOINT is dummy to keep container alive.

## Running the Games Servers

Each game proven to be supported will have a dedicated readme in the top of this repo, under its subdirectory (e.g. stationeers/README.md).