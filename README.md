npm-run-test
============


无意间看到
[forge](https://github.com/digitalbazaar/forge) A native implementation of TLS (and various other cryptographic tools) in JavaScript.

发现它里面的`npm run`命令

我之前只是使用package.json里的scripts里的

- start
- test

我其实还挺好奇，为啥npm支持的命令这么少

## 可重写的命令

```
Usage: npm <command>

where <command> is one of:
    add-user, adduser, apihelp, author, bin, bugs, c, cache,
    completion, config, ddp, dedupe, deprecate, docs, edit,
    explore, faq, find, find-dupes, get, help, help-search,
    home, i, info, init, install, isntall, issues, la, link,
    list, ll, ln, login, ls, outdated, owner, pack, prefix,
    prune, publish, r, rb, rebuild, remove, repo, restart, rm,
    root, run-script, s, se, search, set, show, shrinkwrap,
    star, stars, start, stop, submodule, t, tag, test, tst, un,
    uninstall, unlink, unpublish, unstar, up, update, v,
    version, view, whoami
```

上面我们说的start和test命令就是这样玩的。

## 自定义的命令

从上面的命令列表里我们可以看到，没有index命令，那么我们怎么自定义呢？

先定义package.json里的命令

  "scripts": {
    "test": "npm run index",
		"index":"node index.js"
  },

然后我创建index.js，并在里面加一句打印

	console.log('node index.js');
	
测试

	npm run index
	
结果如下

```
➜  npm-run-test git:(master) ✗ npm run index

> npm-run-test@1.0.0 index /Users/sang/workspace/github/npm-run-test
> node index.js

node index.js
```

自定义命令的规律是

1. 不在npm可重写里的
1. 通过npm run + cmd即可知晓 
1. cmd可以是shell脚本也可以是gulp命令，也可以是nodejs写的脚本

它给力你无限自由

## 组合拳	

先定义package.json里的命令

  "scripts": {
    "test": "npm run index",
		"index":"node index.js"
  },

这里执行

	npm test
	
输出结果如下

```
➜  npm-run-test git:(master) ✗ npm test

> npm-run-test@1.0.0 test /Users/sang/workspace/github/npm-run-test
> npm run index


> npm-run-test@1.0.0 index /Users/sang/workspace/github/npm-run-test
> node index.js

node index.js
```


## Contributing

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request


## 版本历史

- v1.0.0 初始化版本

## 欢迎fork和反馈

- write by `i5ting` shiren1118@126.com

如有建议或意见，请在issue提问或邮件

## License

this repo is released under the [MIT
License](http://www.opensource.org/licenses/MIT).
