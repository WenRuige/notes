介绍一下`ListenAndServe` 函数

```go
func ListenAndServe(addr string, handler Handler) error {
	server := &Server{Addr: addr, Handler: handler} //初始化操作
	return server.ListenAndServe()     				//监听
}
```



此处需要传两个参数

* `addr`(地址):  ip + port
* Handler:处理者,如果传空的话,会默认使用`DefaultServeMux`



简单介绍一下IPV6:2031:0000:1F1F:0000:0000:0100:11A0:ADDF, 采用16进制表示地址

