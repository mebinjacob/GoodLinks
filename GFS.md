
GFS : Google File System
========================

Why are we reading this paper ? 
  The file system used for map/reduce.
  Main themese of 6.824 show up in this paper.
    trading consistency for simplicity and performance. 
    motivation for subsequent designs.
  good system paper -- details from apps all the way to network performance, fault-tolerance, consistency.
  many other systems use GFS (e.g, BigTable, Spanner @ Google)
  HDFS (Hadoop Distributed File System) based on GFS.

What is consistency ?
  A correctness condition
  Important but difficult to achieve when data is replicated
    especially when application access it concurrently 

  If an application writes, what will a later read observe ? 
    what if the read is from a different application ?
  but with replication 

  What is consistency ?
    A correctness condition 
      Important but difficult to achieve  when data is replicated especially when application access it concurrently
      If an application writes, what will a later read observe ? 
        what if the read is from a different application ?
        but with replication, each write mist also happen on other machines 
    Weak Consistency 
      read() may return stale data -- not hte result of the most recent write
    String Consistency
      read() always return stake data -- not the result of the most recent write 

    General tension between these :
      strong consistency is easy for application writers 
      strong consistency is bad for performance.
      weak consistency has good performance and is easy to scale to many servers 
      weak consistency is complex to reason about 
    
    Many trade offs give rise to different correctness conditions
      These are called "consistency models"
      First peek today; will show up in almost every paper we read this term.
    
  "Ideal" consistency model
    Let's go back to the single-machibe case

      Would be nice if a replicated FS behaved like a non-replicated file system.
      If one application writes, later reads will observe that write.

      What if two application concurrently write to the same  file ?
        Q. What happens on a single machine ? 
        In file system oftem undefined -- file may have some mixed content 
      What if two application concurrently write to the same file ? 
        Q. Waht happens on a single machine ?
          One goes first, the other goes second (use locking)

Challenges to achieving ideal consistency 
  Concurrency -- as we just saw; plus there are many disks in reality 
  Machine failures -- any operation can fail to complete 
  Network partitions -- may not be able to reach every machine/disk
  Why are these challenges difficult to overcome ?
    Requires communication between clients and servers 
        May cost performance 
    Protocols can become complex -- see next week 
      Difficult to implement system correctly.
    Many systems in 
