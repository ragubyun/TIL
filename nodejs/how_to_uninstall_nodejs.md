# macOS 에서 Node.js 완벽하게 삭제하는 방법

1. Go to `/usr/local/lib` - delete any `node` and `node_modules`
1. Go to `/usr/local/include` - delete any `node` and `node_modules` directory
1. If you installed with `brew install node` — run `brew uninstall node` in your terminal
1. Check your Home directory for any `local` or `lib` or include folders — delete any `node` or `node_modules` from there
1. Go to `/usr/local/bin` — delete any `node` executable

위 방법으로도 완벽하게 삭제되지 않는다면 아래 명령어들 실행

```shell
1. sudo rm /usr/local/bin/npm
2. sudo rm /usr/local/share/man/man1/node.1
3. sudo rm /usr/local/lib/dtrace/node.d
4. sudo rm -rf ~/.npm
5. sudo rm -rf ~/.node-gyp
6. sudo rm /opt/local/bin/node
7. sudo rm /opt/local/include/node
8. sudo rm -rf /opt/local/lib/node_modules
9. sudo rm -rf /usr/local/include/node/
```

출처 : [How To Completely Uninstall Node.js From Mac OS X](http://benznext.com/completely-uninstall-node-js-from-mac-os-x/)