# Minimal docker-compose file to run CoreDNS

## TL;DR

```sh
docker-compose up -d

docker-compose exec etcd sh -c 'export ETCDCTL_API=3 && etcdctl put /skydns/com/example/host/ {\"host\":\"1.1.1.1\",\"ttl\":60}' 
docker-compose exec etcd sh -c 'export ETCDCTL_API=3 && etcdctl get /skydns/com/example/host/'
```

Check running successfully

```sh
dig @127.0.0.1 host.example.com

; <<>> DiG 9.10.6 <<>> @127.0.0.1 host.example.com
; (1 server found)
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 6199
;; flags: qr aa rd; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1
;; WARNING: recursion requested but not available

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 4096
;; QUESTION SECTION:
;host.example.com.              IN      A

;; ANSWER SECTION:
host.example.com.       60      IN      A       1.1.1.1

;; Query time: 2 msec
;; SERVER: 127.0.0.1#53(127.0.0.1)
;; WHEN: Tue Feb 11 01:24:32 PST 2020
;; MSG SIZE  rcvd: 77
```

## Description

| Contents | Description |
|---|---|
| Corefile | Configuration file for CoreDNS |
| docker-compose.yaml | docker-compose file for easy startup |

## Reference

[Running CoreDNS as a DNS Server in a Container by @robbmanes](https://dev.to/robbmanes/running-coredns-as-a-dns-server-in-a-container-1d0?signin=true)
[CoreDNS etcd plugin document](https://github.com/coredns/coredns/tree/master/plugin/etcd)