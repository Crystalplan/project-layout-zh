# `/pkg`

可以由外部应用使用的库代码(e.g., `/pkg/mypubliclib`)。其他项目将导入这些库，并期望他们正常工作，所以在你放入代码时要三思 :-)。

当你的根目录包含一些非Go组件和目录，它也可以在一个地方将Go代码分组，从而更容易运行各种Go工具（如[`工业编程最佳实践`](https://www.youtube.com/watch?v=PTE4VJIdHPg)中所述）。

注意这个不是普遍接受的模式并且对于使用它的流行项目，你可能找不到10个。由你决定是否要使用这个模式。无论它是否是一个好的模式，更多的人会知道你的想法。它对于新Go开发者有点困惑，但解决这个问题非常简单，这也是该项目层的目标之一。

例子:

* https://github.com/prometheus/prometheus/tree/master/pkg
* https://github.com/istio/istio/tree/master/pkg
* https://github.com/google/gvisor/tree/master/pkg
* https://github.com/google/syzkaller/tree/master/pkg
* https://github.com/perkeep/perkeep/tree/master/pkg
* https://github.com/minio/minio/tree/master/pkg
* https://github.com/heptio/ark/tree/master/pkg
* https://github.com/heptio/sonobuoy/tree/master/pkg
* https://github.com/kubernetes/kubernetes/tree/master/pkg
* https://github.com/moby/moby/tree/master/pkg
* https://github.com/grafana/grafana/tree/master/pkg
* https://github.com/influxdata/influxdb/tree/master/pkg
* https://github.com/coreos/etcd/tree/master/pkg
* https://github.com/oklog/oklog/tree/master/pkg
* https://github.com/flynn/flynn/tree/master/pkg
* https://github.com/jesseduffield/lazygit/tree/master/pkg
* https://github.com/gopasspw/gopass/tree/master/pkg
