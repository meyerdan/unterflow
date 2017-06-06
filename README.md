# unterflow

[![Build Status](https://travis-ci.org/menski/unterflow.svg?branch=master)](https://travis-ci.org/menski/unterflow)

Rust implementation of a to be announced protocol

## unterflow-dump

Dump unterflow network traffic.

### Usage

```bash
$ unterflow-dump --help
unterflow-dump 0.1.0
Dump unterflow protocol packages

USAGE:
    unterflow-dump [FLAGS] [OPTIONS] --interface <interface>

FLAGS:
    -h, --help       Prints help information
    -v               Enable logging, use multiple `v`s to increase verbosity
    -V, --version    Prints version information

OPTIONS:
    -i, --interface <interface>    Interface to capture
    -p, --port <port>              Port to capture [default: 51015]
```

### Example

```bash
$ sudo unterflow-dump -i lo

==>  Packet: 127.0.0.1:41994 -> 127.0.0.1:51015 (160 bytes; seq: 607787046)
FrameHeader { length: 147, version: 0, flags: 0, type_id: Message, stream_id: 2 }
TransportHeader { protocol_id: RequestResponse }
RequestResponseHeader { connection_id: 1, request_id: 0 }
MessageHeader { block_length: 11, template_id: 20, schema_id: 0, version: 1 }
ExecuteCommandRequest { partition_id: 0, key: 18446744073709551615, event_type: TaskEvent, topic_name: "default-topic", command: {"eventType": "CREATE", "retries": 3, "type": "foo", "headers": {"k1": "a", "k2": "b"}, "payload": [129, 167, 112, 97, 121, 108, 111, 97, 100, 123]} }

==>  Packet: 127.0.0.1:51015 -> 127.0.0.1:41994 (288 bytes; seq: 2851114393)
FrameHeader { length: 269, version: 0, flags: 0, type_id: Message, stream_id: 2 }
TransportHeader { protocol_id: RequestResponse }
RequestResponseHeader { connection_id: 1, request_id: 0 }
MessageHeader { block_length: 10, template_id: 21, schema_id: 0, version: 1 }
ExecuteCommandResponse { partition_id: 0, key: 4294967544, topic_name: "default-topic", event: {"eventType": "CREATED", "lockTime": -9223372036854775808, "lockOwner": -1, "retries": 3, "type": "foo", "headers": {"bpmnProcessId": "", "workflowDefinitionVersion": -1, "workflowInstanceKey": -1, "activityId": "", "activityInstanceKey": -1, "customHeaders": [], "k1": "a", "k2": "b"}, "payload": [129, 167, 112, 97, 121, 108, 111, 97, 100, 123]} }

==>  Packet: 127.0.0.1:41994 -> 127.0.0.1:51015 (16 bytes; seq: 607787206)
FrameHeader { length: 0, version: 0, flags: 0, type_id: ControlClose, stream_id: 0 }

==>  Packet: 127.0.0.1:51015 -> 127.0.0.1:41994 (16 bytes; seq: 2851114681)
FrameHeader { length: 0, version: 0, flags: 0, type_id: ControlEndOfStream, stream_id: 0 }
```
