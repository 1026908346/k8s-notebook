# PLEG

## 功能
全称：Pod lifecycle event generator，用于产生pod声明周期中的事件

## 代码逻辑
接口PLEG： pkg/kubelet/pleg/pleg.go:53
```go
// 接口
// PodLifecycleEventGenerator contains functions for generating pod life cycle events.
type PodLifecycleEventGenerator interface {
	Start()
	Watch() chan *PodLifecycleEvent
	Healthy() (bool, error)
}

// 实现
type GenericPLEG struct {
    // The period for relisting.
    relistPeriod time.Duration
    // The container runtime.
    runtime kubecontainer.Runtime
    // The channel from which the subscriber listens events.
    eventChannel chan *PodLifecycleEvent
    // The internal cache for pod/container information.
    podRecords podRecords
    // Time of the last relisting.
    relistTime atomic.Value
    // Cache for storing the runtime states required for syncing pods.
    cache kubecontainer.Cache
    // For testability.
    clock clock.Clock
    // Pods that failed to have their status retrieved during a relist. These pods will be
    // retried during the next relisting.
    podsToReinspect map[types.UID]*kubecontainers.Pod
}
```


```go

//pkg/kubelet/pleg/generic.go:131
//每秒执行g.relist

// 1、event产生过程： 
// 通过list_containers填充缓存old pods
// 后面每秒都会list_containers，判断计算new pod和old pod判断是否产生事件。
// 产生事件后将会发送到plegCh

// 2、event消费过程
// plegCh会在syncLoopIteration函数中被消费
// 消费event时，走dispatchWork流程，后续就交给podWorker处理了
```

