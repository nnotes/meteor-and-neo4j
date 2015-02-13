# STORY-TEMPLATE-VERSION: 4.3.0

* Meteor and neo4j

  - NNotes _expects_ to deal with highly connected data for a reasonable amount
    of resources (dev time, $) _so that_ NNotes can handle the "social" aspect
    of the plateform.



** Context

   - Version: 1.0.0

   - Contribution policy: [[http://rfc.zeromq.org/spec:22][C4.1]]

   - Project style guide: [[https://github.com/nomosyn/resources][Coding style]]

   - short name: db

   - abbreviation: db

   - Licensed under: [[https://www.mozilla.org/MPL/2.0/][MPLv2]]

   - Contributors:
       - Full name: Pierre-Henry Fröhring, contact: frohring.pierrehenry@gmail.com



** Init State

   - MongoDB is nicely integrated with Meteor and we did not have a lot of data
     types to take care of + Meteor has on its roadmap the aim to support more
     DB. => Conclusion: use Mongo, switch later if needed.



** Problem

   - We are about to do a DB migration to let the "old" DB fits the "new" data
     patterns. This is a manual, low-level, (no schema) dangerous (no way to
     inforce invariants in all records) operations.

   - New data is "highly" connected which is notoriously bad to handle in
     mongoDB



** End State

   - Let data be exploaded into "atomic" connected neo4j data nodes then build
     unconnected data useful to clients from "atoms" and store it into MongoDB.

   - When a record changes in MongoDB then ask to neo4j if it's possible to
     modify the corresponding "atoms" accordingly.

   - Reflect neo4j decision in MongoDB.



*** Rationale

    - Deep integration of MongoDB in Meteor...
        - Publish/Subscribe

        - Auto synchronisations amongs clients

    - => Better to build around MongoDB instead of replacing it.
