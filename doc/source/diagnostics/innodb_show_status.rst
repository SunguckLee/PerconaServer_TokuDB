.. _innodb_show_status:

======================================
 Extended Show Engine |InnoDB| Status
======================================

This feature reorganizes the output of ``SHOW ENGINE INNODB STATUS`` for a better readability and prints the amount of memory used by the internal hash tables. In addition, new variables are available to control the output.

This feature modified the ``SHOW ENGINE INNODB STATUS`` command as follows:

  * ``TRANSACTION`` section was moved to the end of the output, so that important information is not overlooked when the there is a large amount of it.

  * Added two variables to control ``SHOW ENGINE INNODB STATUS`` information presented (bugfix for `#29123 <http://bugs.mysql.com/bug.php?id=29123>`_):

    * :variable:`innodb_show_verbose_locks` - Whether to show records locked

    * :variable:`innodb_show_locks_held` - Number of locks held to print for each |InnoDB| transaction

  * Added extended information about |InnoDB| internal hash table sizes (in bytes) in the ``BUFFER POOL AND MEMORY`` section; also added buffer pool size in bytes.

  * Added additional LOG section information.

Version Specific Information
============================

  * :rn:`5.6.11-60.3`:

    Feature ported from |Percona Server| 5.5.


Other Information
=================

  * Author / Origin:
    Baron Schwartz, http://lists.mysql.com/internals/35174


System Variables
================

.. variable:: innodb_show_verbose_locks

     :cli: Yes
     :conf: Yes
     :scope: Global
     :dyn: Yes
     :vartype: ULONG
     :default: 0
     :range: 0 - 1

Specifies to show records locked in ``SHOW ENGINE INNODB STATUS``. The default is 0, which means only the higher-level information about the lock (which table and index is locked, etc.) is printed. If set to 1, then traditional |InnoDB| behavior is enabled: the records that are locked are dumped to the output.

.. variable:: innodb_show_locks_held

     :cli: Yes
     :conf: Yes
     :scope: Global
     :dyn: Yes
     :vartype: ULONG
     :default: 10
     :range: 0 - 1000

Specifies the number of locks held to print for each |InnoDB| transaction in ``SHOW ENGINE INNODB STATUS``.


Status Variables
================

The status variables here contain information available in the output of ``SHOW ENGINE INNODB STATUS``, organized by the sections ``SHOW ENGINE INNODB STATUS`` displays. If you are familiar with the output of ``SHOW ENGINE INNODB STATUS``, you will probably already recognize the information these variables contain.


BACKGROUND THREAD
-----------------

The following variables contain information in the BACKGROUND THREAD section of the output from ``SHOW ENGINE INNODB STATUS``. An example of that output is: :: 

  -----------------
  BACKGROUND THREAD
  -----------------
  srv_master_thread loops: 1 srv_active, 0 srv_shutdown, 11844 srv_idle
  srv_master_thread log flush and writes: 11844


.. variable:: Innodb_master_thread_active_loops

     :version 5.6.11-60.3: Introduced.
     :vartype: Numeric
     :scope: Global

.. variable:: Innodb_master_thread_idle_loops

     :version 5.6.11-60.3: Introduced.
     :vartype: Numeric
     :scope: Global

.. variable:: Innodb_background_log_sync

     :version 5.6.11-60.3: Introduced.
     :vartype: Numeric
     :scope: Global

SEMAPHORES
----------

The following variables contain information in the SEMAPHORES section of the output from ``SHOW ENGINE INNODB STATUS``. An example of that output is: ::

  ----------
  SEMAPHORES
  ----------
  OS WAIT ARRAY INFO: reservation count 9664, signal count 11182
  Mutex spin waits 20599, rounds 223821, OS waits 4479
  RW-shared spins 5155, OS waits 1678; RW-excl spins 5632, OS waits 2592
  Spin rounds per wait: 10.87 mutex, 15.01 RW-shared, 27.19 RW-excl

.. variable:: Innodb_mutex_os_waits

     :version 5.6.11-60.3: Introduced.
     :vartype: Numeric
     :scope: Global

.. variable:: Innodb_mutex_spin_rounds

     :version 5.6.11-60.3: Introduced.
     :vartype: Numeric
     :scope: Global

.. variable:: Innodb_mutex_spin_waits

     :version 5.6.11-60.3: Introduced.
     :vartype: Numeric
     :scope: Global

.. variable:: Innodb_s_lock_os_waits

     :version 5.6.11-60.3: Introduced.
     :vartype: Numeric
     :scope: Global

.. variable:: Innodb_s_lock_spin_rounds

     :version 5.6.11-60.3: Introduced.
     :vartype: Numeric
     :scope: Global

.. variable:: Innodb_s_lock_spin_waits

     :version 5.6.11-60.3: Introduced.
     :vartype: Numeric
     :scope: Global

.. variable:: Innodb_x_lock_os_waits

     :version 5.6.11-60.3: Introduced.
     :vartype: Numeric
     :scope: Global

.. variable:: Innodb_x_lock_spin_rounds

     :version 5.6.11-60.3: Introduced.
     :vartype: Numeric
     :scope: Global

.. variable:: Innodb_x_lock_spin_waits

     :version 5.6.11-60.3: Introduced.
     :vartype: Numeric
     :scope: Global

INSERT BUFFER AND ADAPTIVE HASH INDEX
-------------------------------------

The following variables contain information in the INSERT BUFFER AND ADAPTIVE HASH INDEX section of the output from ``SHOW ENGINE INNODB STATUS``. An example of that output is: ::

  -------------------------------------
  INSERT BUFFER AND ADAPTIVE HASH INDEX
  -------------------------------------
  Ibuf: size 1, free list len 6089, seg size 6091,
  44497 inserts, 44497 merged recs, 8734 merges
  0.00 hash searches/s, 0.00 non-hash searches/s

.. variable:: Innodb_ibuf_discarded_delete_marks

     :version 5.6.11-60.3: Introduced.
     :vartype: Numeric
     :scope: Global

.. variable:: Innodb_ibuf_discarded_deletes

     :version 5.6.11-60.3: Introduced.
     :vartype: Numeric
     :scope: Global

.. variable:: Innodb_ibuf_discarded_inserts

     :version 5.6.11-60.3: Introduced.
     :vartype: Numeric
     :scope: Global

.. variable:: Innodb_ibuf_free_list

     :version 5.6.11-60.3: Introduced.
     :vartype: Numeric
     :scope: Global

.. variable:: Innodb_ibuf_merged_delete_marks

     :version 5.6.11-60.3: Introduced.
     :vartype: Numeric
     :scope: Global

.. variable:: Innodb_ibuf_merged_deletes

     :version 5.6.11-60.3: Introduced.
     :vartype: Numeric
     :scope: Global

.. variable:: Innodb_ibuf_merged_inserts

     :version 5.6.11-60.3: Introduced.
     :vartype: Numeric
     :scope: Global

.. variable:: Innodb_ibuf_merges

     :version 5.6.11-60.3: Introduced.
     :vartype: Numeric
     :scope: Global

.. variable:: Innodb_ibuf_segment_size

     :version 5.6.11-60.3: Introduced.
     :vartype: Numeric
     :scope: Global

.. variable:: Innodb_ibuf_size

     :version 5.6.11-60.3: Introduced.
     :vartype: Numeric
     :scope: Global

LOG
---

The following variables contain information in the LOG section of the output from ``SHOW ENGINE INNODB STATUS``. An example of that output is: ::

  LOG
  ---
  Log sequence number 10145937666
  Log flushed up to   10145937666
  Pages flushed up to 10145937666
  Last checkpoint at  10145937666
  Max checkpoint age    80826164
  Checkpoint age target 78300347
  Modified age          0
  Checkpoint age        0
  0 pending log writes, 0 pending chkp writes
  9 log i/o's done, 0.00 log i/o's/second
  Log tracking enabled
  Log tracked up to   10145937666
  Max tracked LSN age 80826164

.. variable:: Innodb_lsn_current

     :version 5.6.11-60.3: Introduced.
     :vartype: Numeric
     :scope: Global

.. variable:: Innodb_lsn_flushed

     :version 5.6.11-60.3: Introduced.
     :vartype: Numeric
     :scope: Global

.. variable:: Innodb_lsn_last_checkpoint

     :version 5.6.11-60.3: Introduced.
     :vartype: Numeric
     :scope: Global

.. variable:: Innodb_checkpoint_age

     :version 5.6.11-60.3: Introduced.
     :vartype: Numeric
     :scope: Global

.. variable:: Innodb_checkpoint_max_age

     :version 5.6.11-60.3: Introduced.
     :vartype: Numeric
     :scope: Global

BUFFER POOL AND MEMORY
----------------------

The following variables contain information in the BUFFER POOL AND MEMORY section of the output from ``SHOW ENGINE INNODB STATUS``. An example of that output is: ::

  ----------------------
  BUFFER POOL AND MEMORY
  ----------------------
  Total memory allocated 137363456; in additional pool allocated 0
  Total memory allocated by read views 88
  Internal hash tables (constant factor + variable factor)
      Adaptive hash index 2266736         (2213368 + 53368)
      Page hash           139112 (buffer pool 0 only)
      Dictionary cache    729463  (554768 + 174695)
      File system         824800  (812272 + 12528)
      Lock system         333248  (332872 + 376)
      Recovery system     0       (0 + 0)
  Dictionary memory allocated 174695
  Buffer pool size        8191
  Buffer pool size, bytes 134201344
  Free buffers            7481
  Database pages          707
  Old database pages      280
  Modified db pages       0
  Pending reads 0
  Pending writes: LRU 0, flush list 0 single page 0
  Pages made young 0, not young 0
  0.00 youngs/s, 0.00 non-youngs/s
  Pages read 707, created 0, written 1
  0.00 reads/s, 0.00 creates/s, 0.00 writes/s
  No buffer pool page gets since the last printout
  Pages read ahead 0.00/s, evicted without access 0.00/s, Random read ahead 0.00/s
  LRU len: 707, unzip_LRU len: 0


.. variable:: Innodb_mem_adaptive_hash

     :version 5.6.11-60.3: Introduced.
     :vartype: Numeric
     :scope: Global

.. variable:: Innodb_mem_dictionary

     :version 5.6.11-60.3: Introduced.
     :vartype: Numeric
     :scope: Global

.. variable:: Innodb_mem_total

     :version 5.6.11-60.3: Introduced.
     :vartype: Numeric
     :scope: Global

.. variable:: Innodb_buffer_pool_pages_LRU_flushed

     :version 5.6.11-60.3: Introduced.
     :vartype: Numeric
     :scope: Global

.. variable:: Innodb_buffer_pool_pages_made_not_young

     :version 5.6.11-60.3: Introduced.
     :vartype: Numeric
     :scope: Global

.. variable:: Innodb_buffer_pool_pages_made_young

     :version 5.6.11-60.3: Introduced.
     :vartype: Numeric
     :scope: Global

.. variable:: Innodb_buffer_pool_pages_old

     :version 5.6.11-60.3: Introduced.
     :vartype: Numeric
     :scope: Global

.. variable:: Innodb_descriptors_memory

     :version 5.6.11-60.3: Introduced.
     :vartype: Numeric
     :scope: Global

This status variable shows the current size of the descriptors array (in bytes). The descriptor array is an |XtraDB| data structure that contains the information on currently running transactions.

.. variable:: Innodb_read_views_memory

     :version 5.6.11-60.3: Introduced.
     :vartype: Numeric
     :scope: Global

This status variable shows the total amount of memory allocated for the |InnoDB| read view (in bytes).

TRANSACTIONS
------------

The following variables contain information in the TRANSACTIONS section of the output from ``SHOW INNODB STATUS``. An example of that output is: ::

  ------------
  TRANSACTIONS
  ------------
  Trx id counter F561FD
  Purge done for trx's n:o < F561EB undo n:o < 0
  History list length 19
  LIST OF TRANSACTIONS FOR EACH SESSION:
  ---TRANSACTION 0, not started, process no 993, OS thread id 140213152634640
  mysql thread id 15933, query id 32109 localhost root
  show innodb status
  ---TRANSACTION F561FC, ACTIVE 29 sec, process no 993, OS thread id 140213152769808 updating or deleting
  mysql tables in use 1, locked 1


.. variable:: Innodb_history_list_length

     :version 5.6.11-60.3: Introduced.
     :vartype: Numeric
     :scope: Global

.. variable:: Innodb_max_trx_id

     :version 5.6.11-60.3: Introduced.
     :vartype: Numeric
     :scope: Global

.. variable:: Innodb_oldest_view_low_limit_trx_id

     :version 5.6.11-60.3: Introduced.
     :vartype: Numeric
     :scope: Global

.. variable:: Innodb_purge_trx_id

     :version 5.6.11-60.3: Introduced.
     :vartype: Numeric
     :scope: Global

.. variable:: Innodb_purge_undo_no

     :version 5.6.11-60.3: Introduced.
     :vartype: Numeric
     :scope: Global

.. variable:: Innodb_current_row_locks

     :version 5.6.11-60.3: Introduced.
     :vartype: Numeric
     :scope: Global

INFORMATION_SCHEMA Tables
=========================

The following table contains information about the oldest active transaction in the system.

.. table:: INFORMATION_SCHEMA.XTRADB_READ_VIEW

   :column READ_VIEW_UNDO_NUMBER:
   :column READ_VIEW_LOW_LIMIT_TRX_NUMBER: This is the highest transactions number at the time the view was created. 
   :column READ_VIEW_UPPER_LIMIT_TRX_ID: This is the highest transactions ID at the time the view was created. This means that it should not see newer transactions with IDs bigger than or equal to that value.
   :column READ_VIEW_LOW_LIMIT_TRX_ID: This is the latest committed transaction ID at the time the oldest view was created. This means that it should see all transactions with IDs smaller than or equal to that value.

The following table contains information about the memory usage for InnoDB/XtraDB hash tables.

.. table:: INFORMATION_SCHEMA.XTRADB_INTERNAL_HASH_TABLES

   :column INTERNAL_HASH_TABLE_NAME: Hash table name
   :column TOTAL_MEMORY: Total amount of memory
   :column CONSTANT_MEMORY: Constant memory
   :column VARIABLE_MEMORY: Variable memory


Other reading
=============

  * `SHOW INNODB STATUS walk through <http://www.mysqlperformanceblog.com/2006/07/17/show-innodb-status-walk-through/>`_

  * `Table locks in SHOW INNODB STATUS <http://www.mysqlperformanceblog.com/2010/06/08/table-locks-in-show-innodb-status/>`_
