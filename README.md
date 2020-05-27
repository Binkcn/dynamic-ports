# dynamic-ports-switching

### 先挖个坑，等有时间有迫切需要的时候再填，目前有其他东西优先级更高的东西要做。


#### dpss（服务器端，或称为端口改变方）
1. 允许配置端口变化范围规则，比如 2333-2433,3133-3233,3333
2. 允许配置端口变化规则：
     * 允许timer定时自动变化，1min 10min 这样。
     * 触发式变化规则，譬如端口空闲超过指定时间，（netstat -anop | grep 8080 | grep -v LISTEN | wc -l）
3. 配置端口变更方式：
    1. 顺序启用，循环复用
    2. 无序随机，记录使用历史，全部使用过之后，循环复用
4. 变更后执行shell，譬如reload firewall，reload ssr，reload nginx ...
5. 监听特定端口，接受 dpsc 查询，支持设定key验证。

#### dpsc（客户端，或称为端口跟随方）
1. 配置 dpss 的ip和port
2. 定时查询特定服务当前启用的 port 和 timeout
3. 跟随port变更，并执行shell 进行 reload
4. ...
