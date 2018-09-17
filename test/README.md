# `/test`

其他外部测试应用和测试数据。你可以随意构建 `/test` 目录。对于更大的项目，有一个数据子目录是有意义的。例如，如果需要Go忽略该目录中的内容，可以使用 `/test/data` 或 `/test/testdata` 目录。请注意Go也会忽略以"." 或 "_" 开头的目录或文件。因此你在命名测试数据目录方面具有更大的灵活性。

例子:

* https://github.com/openshift/origin/tree/master/test (test data is in the `/testdata` subdirectory)


