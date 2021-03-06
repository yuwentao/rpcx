@andot submitited a pull request [#46](https://github.com/smallnest/rpcx/pull/46) to add benchmark codes of hprose 2.0 rpc framework.

The below is benchmark of [hprose](https://github.com/hprose/hprose-go) and [rpcx](https://github.com/smallnest/rpcx).

## Test Environment
Two aws c4.4xlarge servers. One is for the client and the other is for the server.

Intel(R) Xeon(R) CPU E5-2666 v3 @ 2.90GHz, 16 processors
32G memory


hprose-go version: 2016-10-26

## Test Step
The client uses the below cmd to test:

```sh
./client -c $concurrent -n 1000000 -s 172.31.14.248:9981
```

concurrent is 100, 500, 1000, 2000, 5000.
the total requests are 1,000,000.
The message size is 581 bytes.

I only test end-to-end test case (one client and one server).

## Test Result

### rpcx
concurrent clients|mean(ms)|median(ms)|max(ms)|min(ms)|p99.9|throughput(TPS)
-------------|-------------|-------------|-------------|-------------|------------|-------------
100|0|0|13|0|4|153822
500|2|1|1022|0|9|231000
1000|3|2|3014|0|19|215470
2000|6|3|3013|0|212|253292
5000|17|3|6266|0|1453|124331


### hprose-go 2.0
concurrent clients|mean(ms)|median(ms)|max(ms)|min(ms)|p99.9|throughput(TPS)
-------------|-------------|-------------|-------------|-------------|------------|-------------
100|0|0|8|0|4|126887
500|2|1|28|0|15|169290
1000|5|3|1058|0|33|181983
2000|10|8|1024|0|211|179726
5000|24|7|7201|0|1060|113726



