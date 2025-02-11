---
description: "sys.sp_xtp_unbind_db_resource_pool (Transact-SQL)"
title: "sys.sp_xtp_unbind_db_resource_pool (Transact-SQL) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.service: sql
ms.reviewer: ""
ms.subservice: system-objects
ms.topic: "reference"
f1_keywords: 
  - "sp_xtp_unbind_db_resource_pool_TSQL"
  - "sp_xtp_unbind_db_resource_pool"
  - "sys.sp_xtp_unbind_db_resource_pool_TSQL"
  - "sys.sp_xtp_unbind_db_resource_pool"
dev_langs: 
  - "TSQL"
helpviewer_keywords: 
  - "sp_xtp_unbind_db_resource_pool"
  - "sys.sp_xtp_unbind_db_resource_pool"
ms.assetid: 695a796d-087e-4bc8-99d0-ddc342604c75
author: markingmyname
ms.author: maghan
---
# sys.sp_xtp_unbind_db_resource_pool (Transact-SQL)
[!INCLUDE[sqlserver](../../includes/applies-to-version/sqlserver.md)]

  This system procedure removes an existing binding between a database and a resource pool for purposes of tracking [!INCLUDE[inmemory](../../includes/inmemory-md.md)] memory usage.  If there is no pool currently bound to the specified database, success is returned. When the database is unbound, the previously allocated memory for memory-optimized objects stays allocated to the previous resource pool. You need to restart the database to free up the allocated memory. Once a database is unbound from the resource pool, the binding resorts to the DEFAULT resource pool.  
  
 :::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## Syntax  
  
```sql  
sys.sp_xtp_unbind_db_resource_pool 'database_name'  
```  
  
## Arguments  
 database_name  
 The name of an existing [!INCLUDE[inmemory](../../includes/inmemory-md.md)] enabled database.  
  
#### Parameters  
  
## Messages  
 If database was bound to a named resource pool, the procedure returns successfully. However, You must restart the database for unbinding to take effect.  
 If there is no existing binding for the database specified, `sp_xtp_unbind_db_resource_pool` returns success, but gives the informational message:  
  
```  
Msg 41374, Level 16, State 1, Procedure sp_xtp_unbind_db_resource_pool_internal, Line 140.  
Database 'Hekaton_DB' does not have a binding to a resource pool.  
  
```  
  
## Example  
 The following code unbinds the database Hekaton_DB from the [!INCLUDE[inmemory](../../includes/inmemory-md.md)] resource pool it is bound to.  If Hekaton_DB is not currently bound to a [!INCLUDE[inmemory](../../includes/inmemory-md.md)] resource pool, a message is given. The database must be restarted for the unbinding to take effect.  
  
```sql  
sys.sp_xtp_unbind_db_resource_pool 'Hekaton_DB'  
```  
  
## Requirements  
  
-   The database specified by `database_name` must have a binding to an [!INCLUDE[inmemory](../../includes/inmemory-md.md)] resource pool.  
  
-   Requires CONTROL SERVER permission.  
  
## See Also  
 [Bind a Database with Memory-Optimized Tables to a Resource Pool](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md)   
 [sys.sp_xtp_bind_db_resource_pool &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-xtp-bind-db-resource-pool-transact-sql.md)  
  
  
