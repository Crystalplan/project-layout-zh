# `/cmd`

该项目的主要应用。

每个应用程序的目录名称应与您想要的可执行文件的名称匹配（例如：`/cmd/myapp`）。

不要在这个应用目录中放很多代码。如果你认为代码能导入并在其他项目中使用，那它应该放在 `/pkg` 目录中。如果代码不能重复使用或你不想其他包重复使用，将代码放入 `internal` 目录。如果你会惊讶其他人会做什么，所有要明确你的意图！

通常有一个小 `main` 函数可以导入和调用 `internal` 和 `/pkg` 目录中的代码，而不是其他内容。

例子在 [`/cmd`](cmd/README.md) 目录中。

例子:

* https://github.com/heptio/ark/tree/master/cmd (just a really small `main` function with everything else in packages)
* https://github.com/moby/moby/tree/master/cmd
* https://github.com/prometheus/prometheus/tree/master/cmd
* https://github.com/influxdata/influxdb/tree/master/cmd
* https://github.com/kubernetes/kubernetes/tree/master/cmd

