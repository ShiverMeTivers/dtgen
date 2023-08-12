# dtgen
Docker Traffic Generation Framework

Simulates traffic to web endpoints using docker containers and randomized ip addresses. 
Used to test effectiveness of SIEM solutions or generate networking "noise" to emulate public website traffic in an air gapped network.

# How it works

1. Creates docker networks named *tg-#* per subnet in subnet.conf
   - Disables docker network isolation and disables ip tables masquerade rules
3. Starts a user specified count of docker containers and assigns randomized /16 or /24 address based on subnet.conf
4. Rotates IP addresses used by each docker container based on the user specified rotation interval

# Setup

**Note** 
Ensure net.ipv4.ip_forward is uncommented and is set to one in `/etc/sysctl.conf`

1. Execute `chmod 777 traffic-gen.sh`
2. Execute `chmod 777 config/traffic-gen-functions.sh`
3. Configure desired source subnets in `config/subnets.conf`
   - Traffic will originate from these subnets.
   - See the `subnets.conf` for more information
4. Set **instance count** and **rotation delay** variables in `traffic-gen-functions.sh`
5. Run `./traffic-gen.sh`
