# 用于Sybase 的 Cli 工具

### isql

用于连接 SyBase 数据库的工具

```shell
> isql -U[username] -P[password] -D[database] -S[server_name:port]
```

连接后的执行的Sql

```sql
-- Sql语句支持多行输入，直到输入go后才提交执行
> select * from dbo.GS_GRP
> go
```



### bcp

用于sybase进行的备份工具

```bash
> bcp {[[database_name.][schema].]{table_name | view_name} | "query"}
    {in | out | queryout | format} data_file
    [-m max_errors] [-f format_file] [-x] [-e err_file]
    [-F first_row] [-L last_row] [-b batch_size]
        [-d database_name] [-n] [-c] [-N] [-w] [-V (70 | 80 | 90 )] 
    [-q] [-C { ACP | OEM | RAW | code_page } ] [-t field_term] 
    [-r row_term] [-i input_file] [-o output_file] [-a packet_size]
    [-S [server_name[/instance_name]]] [-U login_id] [-P password]
        [-T] [-v] [-R] [-k] [-E] [-h"hint [,...n]"]
```

E.g.

```bash
> bcp upms..user_view out ./user_vuew.bcp -e 
```

