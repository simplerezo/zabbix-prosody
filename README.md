# Zabbix-Prosody
Zabbix Template for Prosody using "internal" statistics / mod_munin / mod_measure_*

Works with the very good docker image https://github.com/unclev/prosody-docker-extended

# Installation
1. Configure Prosody Server
  - Enable modules measure_client_presence, measure_stanza_counts and munin (in prosody.cfg.lua file)
```
modules_enabled = {
  [...]
                "measure_client_presence";
                "measure_stanza_counts";
                "munin";
}
```
  - Enable statistics (in prosody.cfg.lua file)
```
-- Uncomment to enable statistics
-- For more info see https://prosody.im/doc/statistics
statistics = "internal"
```

2. If you are using prosody-docker-extended, you need to update docker-compose.yml, adding the following line in the "ports:" section:
```
          - "127.0.0.1:4949:4949"
```
And apply changes by using ```docker-compose down; docker-compose up -d```

3. If you are not using prosody-docker-extended, reload prosody configuration by ```prosodyctl reload```

4. Put **prosody_munin.conf** in your zabbix_agentd.conf.d directory of your Prosody Host (/etc/zabbix/zabbix_agentd.conf.d/ on Linux by default) and reload zabbix agent on it

5. Import **zabbix_prosody_template.xml** and link the template in Zabbix to your Prosody host
