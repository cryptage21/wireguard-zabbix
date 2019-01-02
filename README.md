# wireguard-zabbix
Template to monitor WireGuard with Zabbix

Hi,

I tried to create a template to monitor WireGuard with Zabbix.
WireGuard does not really provide any monitoring tool so I had to do with "wg show" commands.

It's probably not perfect so if you want to help I'm interested.

Template provides 2 discovery rules :

Interfaces Discovery (wg0, wg1...) :
- Items to get active peers, total peers, port used and check firewall mark.
- Triggers to check changes on port, fwmark and numbers of clients.
- Graph to monitor active and total peers (even if connections are never released by WG once established).

Peers Discovery (based on public key) :
I had to truncate keys to 10 characters for easy reading. It should not be a problem because they're random.
- Items to get for each endpoint : allowed IPs, IP address, port used, incoming/outgoing traffic, keepalive status and the last handshake.
- Triggers to track changes on allowed IPs, connection port, IP address, keeaplive status and to monitor high traffic and unreachable endpoint.
- Graph to monitor incoming/outgoing network traffic.

This template may work with previous versions of Zabbix but it was tested for Zabbix 4.0 on a Debian 9.6 server.

To make it work you'll need to : 
- add UserParameters (wireguard.conf for example),
- create a discovery script (zabbix_agentd.d/wireguard by default),
- permit execution for user zabbix via sudo.

Have fun.
