# Grunt watch

# Grunt-watch w/Livereload

现在我们已经设置了Grunt与Sass，当我们在CLI中运行`grunt`任务时，这将处理我们所做的编辑。在快速开发中，回到CLI，输入`grunt`然后刷新浏览器会很快变得乏味。

幸运的是，我们有选择。`grunt-contrib-watch`是一个npm包，它将监视我们的Sass文件，当其中一个被触及时，它将运行Grunt任务来处理它。要安装：

```
npm install --save-dev grunt-contrib-watch 
```

作为额外的奖励，我们不仅可以运行一个监视器来处理我们的Sass，还可以监视`.jade`文件的更改。

在`Gruntfile.js`中，我们需要添加一些Grunt任务：

```
module.exports = function(grunt) {
  grunt.initConfig({
    sass: {
      dist: {
        files: {
          'public/stylesheets/style.css': 'sass/style.scss'
        }
      }
    },
    watch: {
      source: {
        files: ['sass/**/*.scss', 'views/**/*.jade'],
        tasks: ['sass'],
        options: {
          livereload: true
        }
      }
    }
  });

  grunt.loadNpmTasks('grunt-contrib-watch');
  grunt.loadNpmTasks('grunt-sass');
  grunt.registerTask('default', ['sass']);
}; 
```

现在我们已经安装了Grunt，有一个功能性的`Gruntfile.js`，我们可以开始编写一些Sass了。

## 在layout.jade中添加Livereload

为了让Live reload在项目中触发，我们需要在`layout.jade`文件中在`<body>`标签的最后添加一个对一个不存在的JavaScript文件的引用。

```
script(src='http://localhost:35729/livereload.js') 
```

在一个新的Express项目中，它会像这样：

```
doctype html
html
  head
    title= title
    link(rel='stylesheet', href='/stylesheets/style.css')
  body
    block content

    script(src='http://localhost:35729/livereload.js') 
```

添加完这些后，回到浏览器并刷新，然后在Sass或Jade中的任何编辑都应该触发Livereload。
