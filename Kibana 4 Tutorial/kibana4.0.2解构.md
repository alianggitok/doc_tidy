# kibana 4.0.2 目录解构


##目录
##/bin/
批处理

##/config/
yaml格式的配置文件

##/node/
node

##/plugins/
kibana 官方建议不要在这里自己写 plugins，因为这里目前还没有稳定下来

##/src/
- app.js
node启动文件，环境配置

- index.js
模块依赖，server

- package.json
kibana项目的报管理文件，依赖声明，版本描述等

###/src/bin/
kibana.js 基于 node 的执行脚本
为什么windows版的也有 .sh文件？

###/src/config/
index.js 模块配置信息
kibana.yml 默认配置信息

###/src/lib/
库加载、配置

###/src/node_modules/
node npm 管理的第三方模块

###/src/public/
- require.config.js
资源加载配置文件，基于requirejs

- index.html
主体文件，宿主

- index.js
核心文件，把包括jquery、d3在内的插件、模块代码合并为这一个文件了

- build.txt
像是个打包文件构建的声明脚本，通过他告知合并引擎合并文件到index.js

- **/bower_components/**
bower管理的组件（字体，插件）

- **/components/**
页面组件（表格、分页、模块、模板、日期插件……）

- **/directives/**
基于angularjs的指令

- **/images/**
页面中引用的图片（logo、loading）

- **/partials/**
页面部件

- ***/plugins/*** <!!
页面模块（页面的布局等都在这里）
kibana官方建议不要在这里自己写plugins

- **/styles/**
样式文件

- **/utils/**
通用工具集

###/src/routes
路由相关配置模块

###/src/views
jade模板



## 工具
### nodejs
- npm
- express
- bower

### requirejs
做资源异步加载及各资源间的依赖，AMD
### angularjs
数据绑定，mvc的实现
