# container-log manager

// TODO: 还没看懂

分析container-log manager源码

`pkg/kubelet/logs/container_log_manager.go`

```go
for _, container := range containers {
	// ...
	// rotateLog分别执行
	// 1、c.cleanupUnusedLogs(logs)，删掉*.tmp等的一些无用文件
	// 2、logs, err = c.removeExcessLogs(logs)，删掉一些文件，确保最多有MaxFiles个文件
	// 3、 c.rotateLatestLog(id, log)，
	//  3.1 把当前日志文件加个时间戳后缀
	//  3.2 让containerd重新生成一个日志文件
	//  3.3 再把rotated文件名改回去？
	c.rotateLog(id, path)
}
```