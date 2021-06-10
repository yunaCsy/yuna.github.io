# 安装hexo
`npm install hexo-cli -g `
+ [npm install EACCES: permission denied出错解决方案](https://www.cnblogs.com/zhenqichai/p/npm-eacces-permission-error-fix.html)
+ [下载nvm](https://www.jianshu.com/p/cb5265434d91)


# hexo源码分支 hexo-sound-code

+ 启动项目 hexo d
+ 文件添加在source/_drafts md文件
+ hexo d  发布 生成public文件


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
