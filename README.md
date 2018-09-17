# Go 项目层规范

翻译自 https://github.com/golang-standards/project-layout 项目，翻译的不好。

这个是 Go 应用程序项目的基础层。它不是核心Go开发团队定义的官方标准。无论如何，在 Go 生态它是一个通用项目层模式。其中一些模式是比其他更受欢迎。它也有一些小优化，以及对于任何足够大的真实项目所共有的几个常见目录。

如果你尝试学习Go，或如果你正在构建一个PoC(概念验证)项目，或一个玩具项目，这个项目层都包括。开始在一些很简单项目（一个 `main` 文件就足够了），随着项目的发展，请记住确保代码结构良好是非常重要，否则你最终会得到一个包含大量依赖项和全局状态的混乱代码。当你有更多人工作在一个项目中，你将需要更多的结构。那个时候介绍包/库的常用方法很重要。

当你有一个开源项目或你知道其他项目从你的项目库中导入代码时，那么有一个私有（也就是`内部`）包和代码很重要。克隆这个库，只保留你需要的。仅仅因为它在那里但不意味着必须全部使用。在每个单个项目都没有必要使用哪些模式。甚至 `vendor` 模式都不是普遍的。

这个项目层是有意通用的，它并不尝试加入特定的Go包结构。

这是社区的努力。如果你看到新模式或你认为某个现有模式需要更新，请开一个新 Issue。

如果你在命名、格式化、样式上需要帮助，请运行 [`gofmt`](https://golang.org/cmd/gofmt/) and [`golint`](https://github.com/golang/lint)。也请确保去阅读 GO 代码风格指南和推荐。

* https://talks.golang.org/2014/names.slide
* https://golang.org/doc/effective_go.html#names
* https://blog.golang.org/package-names
* https://github.com/golang/go/wiki/CodeReviewComments

其他额外的背景信息，请阅读 [`Go Project Layout`](https://medium.com/golang-learn/go-project-layout-e5213cdcfaa2)。

更多关于命名和包组织以及其他代码结构的阅读推荐：

* [GopherCon EU 2018: Peter Bourgon - Best Practices for Industrial Programming](https://www.youtube.com/watch?v=PTE4VJIdHPg)
* [GopherCon Russia 2018: Ashley McNamara + Brian Ketelsen - Go best practices.](https://www.youtube.com/watch?v=MzTcsI6tn-0)
* [GopherCon 2017: Edward Muller - Go Anti-Patterns](https://www.youtube.com/watch?v=ltqV6pDKZD8)
* [GopherCon 2018: Kat Zien - How Do You Structure Your Go Apps](https://www.youtube.com/watch?v=oL6JBUk6tj0)

## Go 目录

### `/cmd`

该项目的主要应用。

每个应用程序的目录名称应与您想要的可执行文件的名称匹配（例如：`/cmd/myapp`）。

不要在这个应用目录中放很多代码。如果你认为代码能导入并在其他项目中使用，那它应该放在 `/pkg` 目录中。如果代码不能重复使用或你不想其他包重复使用，将代码放入 `internal` 目录。如果你会惊讶其他人会做什么，所有要明确你的意图！

通常有一个小 `main` 函数可以导入和调用 `internal` 和 `/pkg` 目录中的代码，而不是其他内容。

例子在 [`/cmd`](cmd/README.md) 目录中。

### `/internal`

私有应用和库代码。这是你不希望其他人在其他应用和库中导入的代码。

在`/internal/app` (e.g., `/internal/app/myapp`) 目录中放你真实应用的代码，这些应用共享的代码放在 `/internal/pkg` 目录中 (e.g., `/internal/pkg/myprivlib`)。

### `/pkg`

可以由外部应用使用的库代码(e.g., `/pkg/mypubliclib`)。其他项目将导入这些库，并期望他们正常工作，所以在你放入代码时要三思 :-)。

当你的根目录包含一些非Go组件和目录，它也可以在一个地方将Go代码分组，从而更容易运行各种Go工具（如[`工业编程最佳实践`](https://www.youtube.com/watch?v=PTE4VJIdHPg)中所述）。

如果你想看那些流行Go项目使用这个项目层模式，请参阅[`/pkg`](pkg/README.md)目录。这个通用层模式，但它并没有被普遍接受，Go社区中的一些人不推荐它。

### `/vendor`

应用依赖（手动管理或通过流行的依赖管理工具像 [`dep`](https://github.com/golang/dep)）。

如果你是建立一个库，不要提交你的应用依赖。

## 服务应用目录

### `/api`

OpenAPI/Swagger 说明，JSON 概要文件，协议定义文件。

有关示例，请参阅 [`/api`](api/README.md)目录。

## Web 应用目录

### `/web`

Web 应用特定组件：web 静态资源，服务端模板和单页应用（SPAs）。

## 通用应用目录

### `/configs`

配置文件模板或默认配置。

在这里放你的 `confd` 或 `consul-template` 模板文件。

### `/init`

初始化系统（systemd, upstart, sysv）和进程管理配置（runit, supervisord）。

### `/scripts`

脚本是去执行各种构建、安装、分析等操作。

这些脚本保持在根级别小而简单的 Makefile (e.g., `https://github.com/hashicorp/terraform/blob/master/Makefile`)。

有关示例，请参阅 [`/scripts`](scripts/README.md) 目录。

### `/build`

包和持续集成。

在 `/build/package` 目录放你的云上（AMI）、容器（Docker）、系统（deb, rpm, pkg）的包配置和脚本。

在`/build/ci` 目录放你的 CI（travis, circle, drone）的配置文件和脚本。注意那些 CI 工具 (e.g., Travis CI) 是非常要求它们的配置文件位置。尝试将配置文件放在 `/build/ci` 目录中，将它们链接到 CI 工具所期望的位置（如果可以）。

### `/deployments`

Iaas，PaaS，系统和容器编排部署配置和模板（docker-compose, kubernetes/helm, mesos, terraform, bosh）。

### `/test`

其他外部测试应用和测试数据。你可以随意构建 `/test` 目录。对于更大的项目，有一个数据子目录是有意义的。例如，如果需要Go忽略该目录中的内容，可以使用 `/test/data` 或 `/test/testdata` 目录。请注意Go也会忽略以"." 或 "_" 开头的目录或文件。因此你在命名测试数据目录方面具有更大的灵活性。

有关示例，请参阅 [`/test`](test/README.md) 目录。

## 其他目录

### `/docs`

设计和用户文档（除了 godoc 生成的文档）。

有关示例，请参阅 [`/docs`](docs/README.md) 目录。

### `/tools`

为这个项目支持的工具。请注意这些工具能引入来自 `/pkg` 和 `/internal` 目录的代码。

有关示例，请参阅 [`/tools`](tools/README.md) 目录。

### `/examples`

为你的应用程序或公开库写的用例。

有关示例，请参阅 [`/examples`](examples/README.md) 目录。

### `/third_party`

外部帮助工具，分支代码或其他第三方实用应用（e.g., Swagger UI）。

### `/githooks`

Git 钩子。

### `/assets`

项目一起使用的其他资源(图片、CSS、Javascript 等)

## 你不应该有的目录

### `/src`

一些 Go 项目有 `src` 文件夹，但它通常发生在当开发者来自Java 世界时，它是一种常用的模式。如果你能帮助你自己尝试不要去采用这个Java模式。你也不希望你的 Go 代码或Go 项目看上去想Java 吧 :-)

不要将项目级别的 `/src` 目录在 Go用于其工作空间的 `/src` 目录混淆，在 [`如何写Go代码`](https://golang.org/doc/code.html) 中有描述关于Go的工作空间。这个 `$GOPATH` 环境变量指向你(当前)的工作空间。这个工作空间包含了顶层目录 `/pkg`、`/bin` 和 `/src` 目录。你的真实项目最终是在 `/src` 下的子目录。所有如果你的项目中有 `/src` 目录，项目路径看上去想这样：`/some/path/to/workspace/src/your_project/src/your_code.go`。请注意在 Go 1.11 可以将你的项目放在 `GOPATH` 之外，但它仍然不意味着使用这种布局模式是个好注意。

## Badges

* [Go Report Card](https://goreportcard.com/) - 它将使用 `gofmt`, `go vet`, `gocyclo`, `golint`, `ineffassign`, `license` 和 `misspell` 扫描你的代码。参考 `github.com/golang-standards/project-layout` 来替换你的项目。
* [GoDoc](http://godoc.org) - 它将提供你 GoDoc 生成文档的在线版本。更改链接以指向你的项目。
* 发布 - 它将显示你项目的最新版本号。更改Github链接以指向你的项目。

[![Go Report Card](https://goreportcard.com/badge/github.com/golang-standards/project-layout?style=flat-square)](https://goreportcard.com/report/github.com/golang-standards/project-layout)
[![Go Doc](https://img.shields.io/badge/godoc-reference-blue.svg?style=flat-square)](http://godoc.org/github.com/golang-standards/project-layout)
[![Release](https://img.shields.io/github/release/golang-standards/project-layout.svg?style=flat-square)](https://github.com/golang-standards/project-layout/releases/latest)

## 注意

一个更具见解性的带有样本和可重用配置的项目模板，脚本和代码是WIP(半成品)。

