# `/build`

包和持续集成。

在 `/build/package` 目录放你的云上（AMI）、容器（Docker）、系统（deb, rpm, pkg）的包配置和脚本。

在`/build/ci` 目录放你的 CI（travis, circle, drone）的配置文件和脚本。注意那些 CI 工具 (e.g., Travis CI) 是非常要求它们的配置文件位置。尝试将配置文件放在 `/build/ci` 目录中，将它们链接到 CI 工具所期望的位置（如果可以）。

例子:

* https://github.com/cockroachdb/cockroach/tree/master/build
