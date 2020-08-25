# docker-postgres-pgpool
Docker compose básico de PostgreSQL con el middleware [Pgpool-II](https://www.pgpool.net/) (_Connection Pooling, In Memory Query Cache_)
 
Enlaces de interés:
- [docker-compose de Bitnami](https://github.com/bitnami/bitnami-docker-pgpool#using-docker-compose)
- [configuración del contenedor de Pgpool](https://github.com/bitnami/bitnami-docker-pgpool#configuration) ([_non-root_](https://docs.bitnami.com/tutorials/work-with-non-root-containers/))
- [añadir fichero de configuración a Pgpool](https://github.com/bitnami/bitnami-docker-pgpool#configuration-file)
- [tutorial de In Memory Query Cache de Pgpool](https://www.pgpool.net/docs/pgpool-II-3.3.7/doc/tutorial-memqcache-en.html#thisis)

## Configuración de In Memory Query Cache de Pgpool
- Cachear solo las tablas especificadas (lista separada por comas, admite regex)  
`white_memqcache_table_list = '.*_cache_ok'`
- NO cachear las tablas especificadas (lista separada por comas, admite regex)  
`black_memqcache_table_list = '.*_cache_ng'`
- NO cachear cuando el resultado supera un tamaño (default 400KB)  
`memqcache_maxcache = 409600`
- Especificar en la propia sentencia que no se cachee  
`/* NO QUERY CACHE */ SELECT * FROM table_cache_ok WHERE a = 1;`
- Cuándo expira (en segundos) un resultado cacheado  (0 significa que no expira)  
`memqcache_expire = 5`

> Nota: en [pgpool-extra.conf](https://github.com/eloyAM/docker-postgres-pgpool/blob/master/pgpool-extra.conf) el parámetro `log_per_node_statement = on`  
> no es realmente necesario. Nos sirve para ver en el log cómo maneja y cachea cada sentencia.
