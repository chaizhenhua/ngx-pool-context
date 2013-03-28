ngx-pool-context
================

#Synopsis

Nginx-pool-context is a module for developer, it provides extra APIs: 
```
void* ngx_pool_get_ctx(ngx_pool_t * pool, ngx_uint_t index);
ngx_int_t ngx_pool_set_ctx(ngx_pool_t * pool, ngx_uint_t index,void * data);

#define ngx_http_get_module_pool_ctx(r, module)     ngx_pool_get_ctx(r->pool, module.index)
#define ngx_http_set_pool_ctx(r, c, module)         ngx_pool_set_ctx(r->pool, module.index, c)
```
To use these APIs must include ```<ngx_pool_context.h>``` in your file. The APIs are used to attach some module context with a pool(```ngx_pool_set_ctx```), and retrieve it later(```ngx_pool_get_ctx```) at any time before the pool is destroyed. In nginx, the request ctx is created on pool and associated with the request. After internal redirect the request ctx was lost. If you want to retrive ctx from previous processing, you can use these APIs.

#Directives

There is only one configuration directive ```pool_context_hash_size```, which set the internal hash table size.
##pool_context_hash_size
**Syntax:**  **pool_context_hash_size** *number*  
**Default:**	1024  
**Context:**	main  

