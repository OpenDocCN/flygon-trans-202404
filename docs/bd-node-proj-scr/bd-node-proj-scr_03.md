# Grunt

# 安装和设置Grunt

Grunt 是Node世界的工作马。如果需要运行任务，那就让Grunt出马。如果你来自Rails世界，Grunt就像是make或者Rake。关于这个任务运行器有大量的文档，但在这个研讨会中，我将专注于让你快速上手应用程序的基础知识。

Grunt 的设置非常简单，只需在项目的根目录中创建一个新的`Gruntfile.js`文件，并添加以下shell语法：

```
module.exports = function(grunt) {
  grunt.initConfig({

    ...

  });

  grunt.loadNpmTasks('<package>');
}; 
```

要运行Grunt，通常需要全局安装Grunt：

```
npm install grunt -g 
```

但是等等！！部署呢？如果我们创建的任务需要在服务器上运行Grunt，我们需要将其作为应用程序的依赖项。因此，让我们将其安装为本地依赖项：

```
npm install --save grunt 
```

使用这个基本结构和安装了Grunt，我们现在可以开始为我们的应用程序添加新功能了。
