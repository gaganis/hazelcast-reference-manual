
### Queue Full Behavior

In the previous Hazelcast releases, WAN replication was dropping the new events if WAN replication event queues are full.
This behavior is configurable starting with the release 3.6. 

There are two different supported behaviors:
 
- `DISCARD_AFTER_MUTATION`: If you select this option, the new WAN events generated by the member are dropped and not replicated to the target cluster
when the WAN event queues are full.   
- `THROW_EXCEPTION`: If you select this option, the WAN queue size is checked before each supported mutating operation (like `IMap#put`, `ICache#put`).
If one the queues of target cluster is full, `WANReplicationQueueFullException` is thrown and the operation is not allowed.

The following is an example configuration:

```xml
<wan-replication name="my-wan-cluster">
  <wan-publisher group-name="test-cluster-1">
    ...
    <queue-full-behavior>DISCARD_AFTER_MUTATION</queue-full-behavior>
  </wan-publisher>
</wan-replication>
```

![image](images/NoteSmall.jpg) ***NOTE:*** *`queue-full-behavior` configuration is optional. Its default value is `DISCARD_AFTER_MUTATION`*.



