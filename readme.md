## Welcome to RestBus.Benchmarks ##

This project tracks various benchmarks for [RestBus](https://github.com/tenor/RestBus) and other messaging libraries.

The excel sheets with the measurement data and generated charts are in the [data](data) folder.  
The source code for the test projects are in the [src](src) folder.

These tests were ran in AWS Cloud East Region on three m4.4xlarge (16 vcpus, 64 GiB memory, 2000 Mbps network throughput) Windows Server 2012 R2 shared EC2 instances.

One machine runs the RabbitMQ server with the 6 default management related plugins. 
The test server is ran on another machine and the test client on the third one.

See the [test plan](test_plan.md) for more information about the tests.

#### Test Notes ####

**MassTransit**

- All consumers are set to have a [prefetch count](https://www.rabbitmq.com/consumer-prefetch.html) of 50, however MassTransit's consumer prefetch count is global.  
- MassTransit's consumers have [publisher confirms](https://www.rabbitmq.com/confirms.html) turned on, and there seems to be no way to turn it off.  

**NServiceBus**

- Increasing the test thread count did not produce any signicant difference in results.
- Increasing [MaximumConcurrencyLevel](https://web.archive.org/web/20160126031741/http://docs.particular.net/nservicebus/operations/tuning) setting increased the number of threads used by NServiceBus but had no noticeable effect on throughput. 

This may be a licensing issue, but [this suggests otherwise](https://web.archive.org/web/20150503165259/http://docs.particular.net/nservicebus/licensing/licensing-limitations).

**RestBus**

- ASP.Net 5 "Bare to the metal mode" means the MVC pipeline was skipped. [Define this symbol to set the mode](https://github.com/tenor/RestBus.Benchmarks/blob/56c801a61874133e26339674fc5894ec0bbb45ba/src/Benchmarks/RabbitMQ/RestBus/RestBusAspNetTestServer/src/RestBusAspNetTestServer/Startup.cs#L1).

- Consumer No-Ack is false for the server but true for the client since No-Ack is required for the [Direct Reply-to](https://www.rabbitmq.com/direct-reply-to.html) feature, which RestBus uses.

## Test Results
### One Way RPC Throughput Test

This test measures how many 2048 byte messages can be sent on a round-trip from one publisher to one subscriber and back.
The throughput measured is one way. i.e. from client to server.

![One Way RPC Test Results](https://raw.githubusercontent.com/tenor/RestBus.Benchmarks/master/images/RabbitMQ/rpc_throughput_20_threads.png)


![One Way RPC Test Results](https://raw.githubusercontent.com/tenor/RestBus.Benchmarks/master/images/RabbitMQ/rpc_throughput_all_threads.png)

### Send Only Throughput Test ###

This test measures how many 2048 byte messages can be sent rapidly by a client, with one server consuming the queue.

![One Way RPC Test Results](https://raw.githubusercontent.com/tenor/RestBus.Benchmarks/master/images/RabbitMQ/sendonly_throughput_20_threads.png)

![One Way RPC Test Results](https://raw.githubusercontent.com/tenor/RestBus.Benchmarks/master/images/RabbitMQ/sendonly_throughput_all_threads.png)

### Payload Throughput Test

This test measures how many MB/s can be sent by a client to a server with varying payload sizes, in an RPC manner.
The client sends messages of various sizes and the server responds with a 200 byte message.  

The objective is to measure the efficiency of scenarios where a client send files of varying sizes to the server, and the server responds with an "OK" once the file is completely received.

![One Way RPC Test Results](https://raw.githubusercontent.com/tenor/RestBus.Benchmarks/master/images/RabbitMQ/payload_throughput_20_threads.png)

### Ease of Use Rating

| Library      | Difficulty  |
|--------------|-------------|
| RestBus      | Easy        |
| EasyNetQ     | Easy        |
| MassTransit  | Moderate    |
| NServiceBus  | Cumbersome  |
