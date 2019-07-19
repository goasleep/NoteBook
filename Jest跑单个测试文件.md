# Jest跑单个测试文件
> 问题背景：当我们使用vue框架进行测试时，使用的是直接运行jest，就会直接测试所有在__tests__目录下的所有测试文件。但往往有时候，我们不需要执行所有的测试文件，那么如何使用jest运行单个测试文件或者是运行非__tests__目录下的文件


遇到第一个问题的第一反应，我就查看官方提供的文档。
官方文档是这样描述的
```
Run unit tests with Jest. Default testMatch is <rootDir>/(tests/unit/**/*.spec.(js|jsx|ts|tsx)|**/__tests__/*.(js|jsx|ts|tsx)) which matches:

Any files in tests/unit that end in .spec.(js|jsx|ts|tsx);
Any js(x)/ts(x) files inside __tests__ directories.
```
通过文档描述，使用jest测试有三个要求
- 测试文件名要以spec结果
- 测试文件后缀为js，jsx，ts，tsx
- 测试文件需要放在tests/unit/目录下或者是/\_\_tests\_\_/目录下
只要满足这三个要求的测试文件，使用运行jest时就会自动执行

同时官方用例提供了一种方式告诉你如何使用jest进行单个文件测试
```
jest my-test #or
jest path/to/my-test.js
```
我们也可以打开jest的执行文件的源码
``` bash
basedir=$(dirname "$(echo "$0" | sed -e 's,\\,/,g')")

case `uname` in
    *CYGWIN*) basedir=`cygpath -w "$basedir"`;;
esac

if [ -x "$basedir/node" ]; then
  "$basedir/node"  "$basedir/../jest/bin/jest.js" "$@"
  ret=$?
else 
  node  "$basedir/../jest/bin/jest.js" "$@"
  ret=$?
fi
exit $ret
```
&emsp;&emsp;可以发现jest文件可以接受一个参数列表，而这一个参数列表就是我们需要执行测试的文件或者需要执行的文件目录。

&emsp;&emsp;到这里我们可以很顺利的运用jest执行我们需要执行的文件。但是我们还是没有改变需要执行的目录，测试文件仍然还需要在__tests__目录下。想到竟然这一个目录被定死了，那么肯定有它的配置文件，那么就看一下它的配置文件。  很容易知道他的配置文件就是package.json。然而这个文件没有我们需要寻找的jest路径的相关信息。然后就去找最顶级的默认配置文档。发现有testMatch这一个属性。
``` json
  "jest": {
    "testEnvironment": "node",
    "setupFiles": [
      "<rootDir>/scripts/testSetup.js"
    ],
    "testMatch": [
      "**/__tests__/**/*.spec.js"
    ]
  },
```

这里很清晰的说明了jest的测试目录，只要修改这一个“testMatch的值”，就可以随心所欲地运行某个我们想运行的文件。

---
&emsp;&emsp;如果仅仅需要测试单个文件。可以使用Node.js提供了一个运行文件的方法(同时也是VSCode的Jest Runner插件使用的方法).该方法提供两个参数，第一个参数为jest.js文件的绝对路径，第二个文件为测试文件的绝对路径。如
```
node "d:/Smith_Peng/project/node_modules/jest/bin/jest.js" "d:/Smith_Peng/project/all/main-spec.js"
```

---
Reference :
vue默认配置文档：https://github.com/vuejs/vue-cli/blob/dev/package.json  
官方文档：https://github.com/vuejs/vue-cli/tree/dev/packages/%40vue/cli-plugin-unit-jest

