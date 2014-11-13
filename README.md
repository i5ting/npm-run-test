npm-run-test
============


无意间看到
[forge](https://github.com/digitalbazaar/forge) A native implementation of TLS (and various other cryptographic tools) in JavaScript.

发现它里面的`npm run`命令

我之前只是使用`package.json`里的`scripts`里的

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

上面我们说的`start`和`test`命令就是这样玩的。

```
  "scripts": {
		"start":"npm publish ."
  },
```

只需要重写里面的具体命令就可以了，然后执行

	npm start

这样就可以发布npm模块了。

## 自定义的命令

从上面的命令列表里我们可以看到，没有`index`命令，那么我们怎么自定义呢？

先定义`package.json`里的命令

```
  "scripts": {
		"index":"node index.js"
  },
```

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
1. 通过`npm run + cmd`即可知晓 
1. cmd可以是`shell脚本`也可以是`gulp命令`，也可以是`nodejs写的脚本`

它给力你无限自由

## 组合拳	

先定义`package.json`里的命令

```
  "scripts": {
    "test": "npm run index",
		"index":"node index.js"
  },
```

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

## 总结

npm命令分2种

- npm自己的命令，可重写
- 自定义的命令，需要使用`npm run`执行


2种可以组合，其他的就请大家自己发挥吧

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
