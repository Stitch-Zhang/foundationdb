.. _release-notes:

#############
Release Notes
#############

7.1.7
=====
* Same as 7.1.6 release with AVX enabled.

7.1.6
=====
* Released with AVX disabled.
* Fixed a fdbserver crash when given invalid knob name. `(PR #7189) <https://github.com/apple/foundationdb/pull/7189>`_
* Fixed a storage server bug that read data after its failure. `(PR #7217) <https://github.com/apple/foundationdb/pull/7217>`_

7.1.5
=====
* Fixed a fdbcli kill bug that was not killing in parallel. `(PR #7150) <https://github.com/apple/foundationdb/pull/7150>`_
* Fixed a bug that prevents a peer from sending messages on a previously incompatible connection. `(PR #7124) <https://github.com/apple/foundationdb/pull/7124>`_
* Added rocksdb throttling counters to trace event. `(PR #7096) <https://github.com/apple/foundationdb/pull/7096>`_
* Added a backtrace before throwing serialization_failed. `(PR #7155) <https://github.com/apple/foundationdb/pull/7155>`_

7.1.4
=====
* Fixed a bug that prevents client from connecting to a cluster. `(PR #7060) <https://github.com/apple/foundationdb/pull/7060>`_
* Fixed a performance bug that overloads Resolver CPU. `(PR #7068) <https://github.com/apple/foundationdb/pull/7068>`_
* Optimized storage server performance for "get range and flat map" feature. `(PR #7078) <https://github.com/apple/foundationdb/pull/7078>`_
* Optimized both Proxy performance and Resolver (when version vector is enabled) performance. `(PR #7076) <https://github.com/apple/foundationdb/pull/7076>`_
* Fixed a key size limit bug when using tenants. `(PR #6986) <https://github.com/apple/foundationdb/pull/6986>`_
* Fixed operation_failed thrown incorrectly from transactions. `(PR #6993) <https://github.com/apple/foundationdb/pull/6993>`_
* Fixed a version vector bug when GRV cache is used. `(PR #7057) <https://github.com/apple/foundationdb/pull/7057>`_
* Fixed orphaned storage server due to force recovery. `(PR #7028) <https://github.com/apple/foundationdb/pull/7028>`_
* Fixed a bug that a storage server reads stale cluster ID. `(PR #7026) <https://github.com/apple/foundationdb/pull/7026>`_
* Fixed a storage server exclusion status bug that affects wiggling. `(PR #6984) <https://github.com/apple/foundationdb/pull/6984>`_
* Fixed a bug that relocate shard tasks move data to a removed team. `(PR #7023) <https://github.com/apple/foundationdb/pull/7023>`_
* Fixed recruitment thrashing when there are temporarily multiple cluster controllers. `(PR #7001) <https://github.com/apple/foundationdb/pull/7001>`_
* Fixed change feed deletion due to multiple sources race. `(PR #6987) <https://github.com/apple/foundationdb/pull/6987>`_
* Fixed TLog crash if more TLogs are absent than the replication factor. `(PR #6991) <https://github.com/apple/foundationdb/pull/6991>`_
* Added hostname DNS resolution logic for cluster connection string. `(PR #6998) <https://github.com/apple/foundationdb/pull/6998>`_
* Fixed a limit bug in indexPrefetch. `(PR #7005) <https://github.com/apple/foundationdb/pull/7005>`_

7.1.3
=====
* Added logging measuring commit compute duration. `(PR #6906) <https://github.com/apple/foundationdb/pull/6906>`_
* RocksDb used aggregated property metrics for pending compaction bytes. `(PR #6867) <https://github.com/apple/foundationdb/pull/6867>`_
* Fixed a perpetual wiggle bug that would not react to a pause. `(PR #6933) <https://github.com/apple/foundationdb/pull/6933>`_
* Fixed a crash of data distributor. `(PR #6938) <https://github.com/apple/foundationdb/pull/6938>`_
* Added new c libs to client package. `(PR #6921) <https://github.com/apple/foundationdb/pull/6921>`_
* Fixed a bug that prevents a cluster from fully recovered state after taking a snapshot. `(PR #6892) <https://github.com/apple/foundationdb/pull/6892>`_

7.1.2
=====
* Fixed failing upgrades due to non-persisted initial cluster version. `(PR #6864) <https://github.com/apple/foundationdb/pull/6864>`_
* Fixed a client load balancing bug because ClientDBInfo may be unintentionally not set. `(PR #6878) <https://github.com/apple/foundationdb/pull/6878>`_
* Fixed stuck LogRouter due to races of multiple PeekStream requests. `(PR #6870) <https://github.com/apple/foundationdb/pull/6870>`_
* Fixed a client-side infinite loop due to provisional GRV Proxy ID not set in GetReadVersionReply. `(PR #6849) <https://github.com/apple/foundationdb/pull/6849>`_

7.1.1
=====
* Added new c libs to client package. `(PR #6828) <https://github.com/apple/foundationdb/pull/6828>`_

7.1.0
=====

Features
--------
* Added ``USE_GRV_CACHE`` transaction option to allow read versions to be locally cached on the client side for latency optimizations. `(PR #5725) <https://github.com/apple/foundationdb/pull/5725>`_ `(PR #6664) <https://github.com/apple/foundationdb/pull/6664>`_
* Added "get range and flat map" feature with new APIs (see Bindings section). Storage servers are able to generate the keys in the queries based on another query. With this, upper layer can push some computations down to FDB, to improve latency and bandwidth when read. `(PR #5609) <https://github.com/apple/foundationdb/pull/5609>`_, `(PR #6181) <https://github.com/apple/foundationdb/pull/6181>`_, etc..

Performance
-----------

Reliability
-----------

Fixes
-----

Status
------
* Added ``cluster.storage_wiggler`` field report storage wiggle stats `(PR #6219) <https://github.com/apple/foundationdb/pull/6219>`_

Bindings
--------
* C: Added ``fdb_transaction_get_range_and_flat_map`` function to support running queries based on another query in one request. `(PR #5609) <https://github.com/apple/foundationdb/pull/5609>`_
* Java: Added ``Transaction.getRangeAndFlatMap`` function to support running queries based on another query in one request. `(PR #5609) <https://github.com/apple/foundationdb/pull/5609>`_

Other Changes
-------------
* OpenTracing support is now deprecated in favor of OpenTelemetry tracing, which will be enabled in a future release. `(PR #6478) <https://github.com/apple/foundationdb/pull/6478/files>`_
* Changed ``memory`` option to limit resident memory instead of virtual memory. Added a new ``memory_vsize`` option if limiting virtual memory is desired. `(PR #6719) <https://github.com/apple/foundationdb/pull/6719>`_
* Change ``perpetual storage wiggle`` to wiggle the storage servers based on their created time. `(PR #6219) <https://github.com/apple/foundationdb/pull/6219>`_

Earlier release notes
---------------------
* :doc:`7.0 (API Version 700) </release-notes/release-notes-700>`
* :doc:`6.3 (API Version 630) </release-notes/release-notes-630>`
* :doc:`6.2 (API Version 620) </release-notes/release-notes-620>`
* :doc:`6.1 (API Version 610) </release-notes/release-notes-610>`
* :doc:`6.0 (API Version 600) </release-notes/release-notes-600>`
* :doc:`5.2 (API Version 520) </release-notes/release-notes-520>`
* :doc:`5.1 (API Version 510) </release-notes/release-notes-510>`
* :doc:`5.0 (API Version 500) </release-notes/release-notes-500>`
* :doc:`4.6 (API Version 460) </release-notes/release-notes-460>`
* :doc:`4.5 (API Version 450) </release-notes/release-notes-450>`
* :doc:`4.4 (API Version 440) </release-notes/release-notes-440>`
* :doc:`4.3 (API Version 430) </release-notes/release-notes-430>`
* :doc:`4.2 (API Version 420) </release-notes/release-notes-420>`
* :doc:`4.1 (API Version 410) </release-notes/release-notes-410>`
* :doc:`4.0 (API Version 400) </release-notes/release-notes-400>`
* :doc:`3.0 (API Version 300) </release-notes/release-notes-300>`
* :doc:`2.0 (API Version 200) </release-notes/release-notes-200>`
* :doc:`1.0 (API Version 100) </release-notes/release-notes-100>`
* :doc:`Beta 3 (API Version 23) </release-notes/release-notes-023>`
* :doc:`Beta 2 (API Version 22) </release-notes/release-notes-022>`
* :doc:`Beta 1 (API Version 21) </release-notes/release-notes-021>`
* :doc:`Alpha 6 (API Version 16) </release-notes/release-notes-016>`
* :doc:`Alpha 5 (API Version 14) </release-notes/release-notes-014>`
