# tomesh.net Chat

Toronto Mesh is running a [Matrix](http://matrix.org) homeserver for our decentralized chat. The Matrix protocol allows us to communicate on the same homeserver, as well as reach users and rooms on other homeservers via homeserver federation. Users are free to connect to our homeserver with [any compatible desktop or mobile client](http://matrix.org/docs/projects/try-matrix-now.html#clients), or the web client we host.

**Matrix homeserver**: [https://matrix.tomesh.net](https://matrix.tomesh.net)

**Web client**: [https://chat.tomesh.net](https://chat.tomesh.net)

This page describes how both these components are set up.

## Set Up Matrix Homeserver

We currently run the Python-implemented [Synapse](https://github.com/matrix-org/synapse/) homeserver at **matrix.tomesh.net**.

### Install Synapse Homeserver

We are using Terraform to provision our Synapse Homeserver.
The instructions can be found on our [mesh-services repository](https://github.com/tomeshnet/mesh-services/tree/master/matrix-synapse-riot)

### Update Synapse Version

1. SSH into matrix.tomesh.net

1. Update Synapse using Debian's apt command

       sudo apt update && sudo apt dist-upgrade -y

### Synapse Performance Bug

Our version of Synapse homeserver accumulates forward extremities over time due to [a known bug](https://github.com/matrix-org/synapse/issues/1760).
Without the workaround the performance will suffer noticably.
The current workaround is enabling `cleanup_extremities_with_dummy_events` but if that is not working follow steps below:

1. SSH into matrix.tomesh.net

1. Stop the synapse service `sudo systemctl stop matrix-synapse`

1. Switch to Synapse Postgres user `sudo -i -u postgres`

1. Load CLI and connect to Synapse database `psql -d synapse`

1. Run query and look for rooms with more than 3 forward extremities:

	```
	select room_id, count(*) c from event_forward_extremities group by room_id order by c desc limit 30;
	```

1. Run the following for each of the high extremities room:

	```
	DELETE FROM event_forward_extremities AS e
	USING ( 
	    SELECT DISTINCT ON (room_id)
	    room_id,
	    last_value(event_id) OVER w AS event_id
	    FROM event_forward_extremities
	    NATURAL JOIN events
	    WINDOW w AS (
	        PARTITION BY room_id
	        ORDER BY stream_ordering
	        range between unbounded preceding and unbounded following
	    )
	    ORDER BY room_id, stream_ordering
	) AS s
	WHERE
	    s.room_id = e.room_id
	    AND e.event_id != s.event_id
	    AND e.room_id = '!jpZMojebDLgJdJzFWn:matrix.org';
	```

1. Run the select again to confirm that forward extremities counts are cleared up for all those rooms.
 
1. Start Synapse `sudo systemctl start matrix-synapse` and the you should see improved performance and system load of the VM will drop.

### Grant Synapse User Admin Rights
1. SSH into matrix.tomesh.net

1. Switch to Postgres user `sudo -i -u postgres`

1. Load CLI and connect to Synapse database `psql -d synapse`

1. Run the query to make the user an admin replace USERNAME with the username of the user:
	```
	UPDATE users SET admin=1 WHERE name LIKE '@USERNAME:tomesh.net';
	```

### Purging Old Posts and Media Files From One Year Ago
1. Login as an admin user at https://chat.tomesh.net and copy your `Access token`

1. SSH into **matrix.tomesh.net**

1. Put your `Access token` into a variable called `access_token`:

       access_token=ABCD1234...

1. Run the API call to purge old posts (e.g. `#tomesh:tomesh.net` channel with the `Internal room ID:` `!FsFLbKGMcUXEMBxZdu:tomesh.net`).
    To purge another room, replace the ID with that room's ID:

       curl -XPOST -d '{"delete_local_events": true, "purge_up_to_ts": '$(echo $(($(date --date="1 year ago" -u +%s%N)/1000000)))' }' 'http://localhost:8008/_matrix/client/r0/admin/purge_history/!FsFLbKGMcUXEMBxZdu:tomesh.net?access_token='$access_token

1. Optionally you can remove all remote content by running:

       curl -XPOST -d '{}' "http://localhost:8008/_matrix/client/r0/admin/purge_media_cache?before_ts=$(echo $(($(date -u +%s%N)/1000000)))&access_token=$access_token"

1. Switch to Postgres user `sudo -i -u postgres`

1. Load CLI and connect to Synapse database `psql -d synapse`

1. Run the command `VACUUM;`

1. Logout of the database and the Postgres user and return back to your shell

1. Switch to the root user `sudo -i`

1. Go into Synapse's media storage directory

       cd /var/lib/matrix-synapse/media/local_content/

1. Delete old media files by running the following commands:

       cd /var/lib/matrix-synapse/media/local_content/
       find * -mindepth 1 -mtime +365 -delete


### Update Riot Web Client
1. SSH into matrix.tomesh.net

1. Get a root shell with `sudo -i`

1. Download the pre-compiled [Riot Web release](https://github.com/vector-im/riot-web/releases):

       wget https://github.com/vector-im/riot-web/releases/download/v1.3.0/riot-v1.3.0.tar.gz

1. Backup config file

       cp /var/www/chat.tomesh.net/public/config.json /root/riot-config.json

1. Remove old Riot client:

       rm -r /var/www/chat.tomesh.net/public/*

1. Extract **riot-v1.3.0.tar.gz** into **/var/www/chat.tomesh.net/public**:

       tar xf riot-v1.3.0.tar.gz -C /var/www/chat.tomesh.net/public --strip-components 1

1. Restore config file

       cp /root/riot-config.json /var/www/chat.tomesh.net/public/config.json

1. Run `chown -R www-data:www-data /var/www/` to ensure that www-data have full access
