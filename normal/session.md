# session 存储的三种方式
1. stick 粘滞：对同一个用户请求转发到同一台机器上
2. 集中式存储：如 session 共享就集中存储在一个集群上，每台机器去集群上 get 信息就行
3. token：相比集中式存储，token 就显得比较轻巧，它是不需要额外的存储，利用的是加密、解密的思想，在请求中就携带了相关信息，所以就不需要再去查了。