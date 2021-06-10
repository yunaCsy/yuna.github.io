# 安装hexo
`npm install hexo-cli -g `
+ [npm install EACCES: permission denied出错解决方案](https://www.cnblogs.com/zhenqichai/p/npm-eacces-permission-error-fix.html)
+ [下载nvm](https://www.jianshu.com/p/cb5265434d91)


# hexo源码分支 hexo-sound-code

+ 启动项目 hexo s
+ 文件添加在source/_drafts md文件
+ hexo d  发布 生成public文件并发布至github（配置_config.yml）
+ 
```yml
## _config.yml
deploy:
  type: git
  repository: https://github.com/yunahome/yunahome.github.io
  branch: master
```


**文件结构**
```
├── .deploy       # 需要部署的文件
├── node_modules  # 项目所有的依赖包和插件
├── public        # 生成的静态网页文件
├── scaffolds     # 文章模板
├── source        # 博客正文和其他源文件等都应该放在这里
|   ├── _drafts   # 草稿
|   └── _posts    # 文章
├── themes        # 主题
├── _config.yml   # 全局配置文件
└── package.json  # 项目依赖信息
```

# hexo发布分支 master


# 主题 next
下载主题 放入themes
`git clone https://github.com/theme-next/hexo-theme-next themes/next`



# hexo 跟新版本
```
===更新 hexo: 进入 blog 目录，执行如下命令=== 
# 更新 package.json 中的 hexo 及个插件版本

cnpm install -g npm-check           # 检查之前安装的插件，都有哪些是可以升级的 
cnpm install -g npm-upgrade         # 升级系统中的插件
npm-check
npm-upgrade
```

**更新 hexo 及所有插件**
`npm update`

**确认 hexo 已经更新**
`hexo -v`
