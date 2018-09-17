# `/internal`

私有应用和库代码。这是你不希望其他人在其他应用和库中导入的代码。

在`/internal/app` (e.g., `/internal/app/myapp`) 目录中放你真实应用的代码，这些应用共享的代码放在 `/internal/pkg` 目录中 (e.g., `/internal/pkg/myprivlib`)。

例子：

* https://github.com/nsqio/nsq/tree/master/internal