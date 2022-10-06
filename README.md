# Tor
## Configure (Private Obfuscated) Tor Bridges

Tor bridges are secret Tor relays that keep your connection to the Tor network hidden. Bridges are to set as your first tor relay if connection to The Onion Network is blocked or censored. BridgeDb can provide bridges with several types of Pluggable Transports, which can help obfuscate your connections to the Tor Network, making it more difficult for anyone watching your internet traffic to determine that you are using Tor.

##### [Get Bridges](https://bridges.torproject.org/)
> or alternatively email to bridges@torproject.org. Leave the email subject empty and write "get vanilla" in the email's message body. (acceptable providers: providers: [Riseup](https://riseup.net/) or [Gmail](https://mail.google.com/))



### Configure Bridges in TOR-Browser

It is also possible to only use bridges over the Browsers that support them. [Brave Browser](https://brave.com/download/) is used for an example:
Simply head over to setting -> Privacy and security -> Use Bridges
<img width="1440" alt="Untitled" src="https://user-images.githubusercontent.com/107116406/194323292-1e8aad3a-ceff-46b5-9bfd-d4740259ee6e.png">



### Snowflake 

[Snowflake](https://github.com/keroserene/snowflake) is currently deployed as a pluggable transport for Tor.
They have more documentation in the [Snowflake](https://gitlab.torproject.org/tpo/anti-censorship/pluggable-transports/snowflake/-/wikis/home) wiki and at https://snowflake.torproject.org/.

#### Running the Snowflake client with Tor

Clone the repository:
```git clone https://github.com/keroserene/snowflake```

Head to the directory and then "client":

```
cd snowflake/client/
```

Make sure you have [golang](https://github.com/golang/go) installed on your machine and then run:
```go get```
and 
```go build```

Edit the [torrc](https://2019.www.torproject.org/docs/tor-manual.html.en) with your preferred editor:

```
vim torrc
```

```
UseBridges 1

DataDirectory datadir

ClientTransportPlugin snowflake exec ./client -log snowflake.log

Bridge snowflake 127.0.0.1:8118 2B280B23E1107BB62ABFC40DDCC8824814F80A72 fingerprint=2B280B23E1107BB62ABFC40DDCC8824814F80A72 url=https://snowflake-broker.torproject.net.global.prod.fastly.net/ front=cdn.sstatic.net ice=stun:stun.voip.blackberry.com:3478,stun:stun.altar.com.pl:3478,stun:stun.antisip.com:3478,stun:stun.bluesip.net:3478,stun:stun.dus.net:3478,stun:stun.epygi.com:3478,stun:stun.sonetel.com:3478,stun:stun.sonetel.net:3478,stun:stun.stunprotocol.org:3478,stun:stun.uls.co.za:3478,stun:stun.voipgate.com:3478,stun:stun.voys.nl:3478

SocksPort 8118
```
Your torrc in snowflake/client/ should be looking like this.
> more info at:https://github.com/keroserene/snowflake/tree/master/client

At last run:
```tor -f torrc```
and it shouldn't get long until you see "Bootstrapped 100% (done): Done" on your terminal.

