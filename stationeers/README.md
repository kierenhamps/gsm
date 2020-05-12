# STATIONEERS

See [README.md](README.md) for details of the container.
This page is dedicated on how to create the Stationeers dedicated games server using this container.

## Running Stationeers

Create the following directory
```
# Edit the configuration files as necessary.
# Ensure you change:
#  - in stationeers/default.ini:
#    - SERVERNAME - This is displayed in the game join menu
#    - PASSWORD - This is the password to join the game
#    - RCONPASSWORD - This is the remote administration password. Note this port must be forwarded for the gameserver to work so ensure this is long and secure.
#    - GAMEPORT - This I assume is needed to be forwarded in from the internet. This is what remote administration is performed over.
#    - UPDATERPORT - This I also assume needs to be forwarded in from the internet. No idea what it is for though.

# Start the server container
# Note the ports published with `-p` must match those in the default.ini config above.
docker run --name Stationeers --hostname Stationeers -p 27500:27500 -p 27015:27015 -v `pwd`/stationeers/:/home/gsm/lgsm/config-lgsm/stserver/:rw -v `pwd`/stationeers/default.ini:/home/gsm/serverfiles/default.ini:ro -v `pwd`/stationeers/saves:/home/gsm/serverfiles/saves:rw -v `pwd`/stationeers/mods:/home/gsm/serverfiles/mods:rw -d gsm:latest

# Then jump back into the container and install Stationeers
docker exec -it Stationeers bash
# (inside container)
./stserver auto-install
./stserver start
# Get status
./stserver details
```

You can stop the server with:
```
./stserver stop
```

Or just stop the container with:
```
docker stop Stationeers
```

## Edit configuration
The Configuration is stored under the folder stationeers/. There are three files:

common.cfg (the settings for this server)
stserver.cfg (the settings for this instance)
default.ini (config for server settings (lgsm))

If there is only one instance/server running and there will not be any other server it doesn't matter if you change the settings in common.cfg or stserver.cfg. If you planing to run more than on server or instance on the same VM you have to consider if the setting should apply server wide (all instances), or just for a specific Stationeers instance.

NOTE: These should/could be created and COPY'd into the container at build time.

## Example: Change map to Mars
Use your favorite texteditor (ex. vi or nano) and open the _default.cfg (remember not to do any changes here) search for the setting you want to change and copy the text. In our example it is this:

  worldtype="Moon"
  worldname="moon_save"

Now open the file you want to configure. If you want any instance to run a Mars map use common.cfg or if only one instance should run this map use stserver.cfg (or stserver-2.cfg for the next instance). Paste the text at the end of the file and change "Moon" to "Mars"

  worldtype="Mars"
  worldname="mars_save"

Now restart your server with ./stserver restart
Make sure you also change the worldname (this is the folder where the savegame is) if the savegame-file is for a different world than the config is set to the server will not start.

## Remote Administrator

You can send commands on web browser.

Link : http://[dedicated server address]:[GamePort]
