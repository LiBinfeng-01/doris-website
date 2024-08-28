---
{
    "title": "table_properties",
    "language": "en"
}
---

<!--
Licensed to the Apache Software Foundation (ASF) under one
or more contributor license agreements.  See the NOTICE file
distributed with this work for additional information
regarding copyright ownership.  The ASF licenses this file
to you under the Apache License, Version 2.0 (the
"License"); you may not use this file except in compliance
with the License.  You may obtain a copy of the License at

  http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing,
software distributed under the License is distributed on an
"AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
KIND, either express or implied.  See the License for the
specific language governing permissions and limitations
under the License.
-->

### Overview

Used to view the properties of tables (including internal and external tables).

:::tip
This system table is supported from versions 2.1.6 and 3.0.2.
:::

### Database

`information_schema`

### Table Information

| Column Name     | Type         | Description         |
|-----------------|--------------|---------------------|
| TABLE_CATALOG   | VARCHAR(64)  | Catalog to which the table belongs |
| TABLE_SCHEMA    | VARCHAR(64)  | Database to which the table belongs |
| TABLE_NAME      | VARCHAR(64)  | Name of the table |
| PROPERTY_NAME   | STRING       | Name of the property |
| PROPERTY_VALUE  | STRING       | Value of the property |

:::tip
For specific details on table properties, refer to the **Create Table** documentation.
:::

### Examples

1. Query all table properties

    ```
    mysql> select * from information_schema.table_properties;
    +---------------+---------------+----------------------+------------------------------------------------+-------------------------+
    | TABLE_CATALOG | TABLE_SCHEMA  | TABLE_NAME           | PROPERTY_NAME                                  | PROPERTY_VALUE          |
    +---------------+---------------+----------------------+------------------------------------------------+-------------------------+
    ...
    | internal      | test_database | test_table           | min_load_replica_num                           | -1                      |
    | internal      | test_database | test_table           | data_sort.col_num                              | 3                       |
    | internal      | test_database | test_table           | group_commit_interval_ms                       | 10000                   |
    | internal      | test_database | test_table           | data_sort.sort_type                            | LEXICAL                 |
    | internal      | test_database | test_table           | is_being_synced                                | false                   |
    | internal      | test_database | test_table           | binlog.enable                                  | false                   |
    | internal      | test_database | test_table           | enable_mow_light_delete                        | false                   |
    | internal      | test_database | test_table           | binlog.ttl_seconds                             | 86400                   |
    | internal      | test_database | test_table           | inverted_index_storage_format                  | V2                      |
    | internal      | test_database | test_table           | time_series_compaction_empty_rowsets_threshold | 5                       |
    | internal      | test_database | test_table           | default.replication_allocation                 | tag.location.default: 1 |
    | internal      | test_database | test_table           | time_series_compaction_level_threshold         | 1                       |
    | internal      | test_database | test_table           | time_series_compaction_time_threshold_seconds  | 3600                    |
    | internal      | test_database | test_table           | storage_format                                 | V2                      |
    | internal      | test_database | test_table           | store_row_column                               | false                   |
    | internal      | test_database | test_table           | light_schema_change                            | true                    |
    | internal      | test_database | test_table           | enable_unique_key_merge_on_write               | false                   |
    | internal      | test_database | test_table           | in_memory                                      | false                   |
    | internal      | test_database | test_table           | file_cache_ttl_seconds                         | 0                       |
    | internal      | test_database | test_table           | group_commit_data_bytes                        | 134217728               |
    | internal      | test_database | test_table           | compaction_policy                              | size_based              |
    | internal      | test_database | test_table           | _auto_bucket                                   | false                   |
    | internal      | test_database | test_table           | binlog.max_history_nums                        | 9223372036854775807     |
    | internal      | test_database | test_table           | time_series_compaction_file_count_threshold    | 2000                    |
    | internal      | test_database | test_table           | skip_write_index_on_load                       | false                   |
    | internal      | test_database | test_table           | disable_auto_compaction                        | false                   |
    | internal      | test_database | test_table           | row_store_page_size                            | 16384                   |
    | internal      | test_database | test_table           | time_series_compaction_goal_size_mbytes        | 1024                    |
    | internal      | test_database | test_table           | storage_medium                                 | HDD                     |
    | internal      | test_database | test_table           | enable_single_replica_compaction               | false                   |
    | internal      | test_database | test_table           | compression                                    | LZ4F                    |
    | internal      | test_database | test_table           | binlog.max_bytes                               | 9223372036854775807     |
    +---------------+---------------+----------------------+------------------------------------------------+-------------------------+
    ```

2. Query the default replication number

    ```
    mysql> select * from information_schema.table_properties where PROPERTY_NAME="default.replication_allocation";
    +---------------+----------------------+----------------------+--------------------------------+-------------------------+
    | TABLE_CATALOG | TABLE_SCHEMA         | TABLE_NAME           | PROPERTY_NAME                  | PROPERTY_VALUE          |
    +---------------+----------------------+----------------------+--------------------------------+-------------------------+
    | internal      | __internal_schema    | column_statistics    | default.replication_allocation | tag.location.default: 1 |
    | internal      | __internal_schema    | partition_statistics | default.replication_allocation | tag.location.default: 1 |
    | internal      | __internal_schema    | audit_log            | default.replication_allocation | tag.location.default: 1 |
    | internal      | test_database        | test_table           | default.replication_allocation | tag.location.default: 1 |
    +---------------+----------------------+----------------------+--------------------------------+-------------------------+
    ```