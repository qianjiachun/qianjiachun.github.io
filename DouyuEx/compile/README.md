## 如何维护与编译

### 结构
- 本脚本将各个功能分为单独的模块，每个模块互相独立，在"编译"的时候将模块内的代码复制到main.js的相应位置即可
- 使用子模块需在父模块中注册，形式通常为`initPkg_父模块名_子模块名()`
- main.js中默认插入了一个图标，点击图标后展开功能面板。此处为底层设计好的，请慎改
- common.js为一些公共函数，是每个模块都可能会用到的。

### 维护（增加新功能）
1. 在packages内新建一个新的目录作为模块名（大驼峰）
2. 目录下新建相应的js与css文件
3. 每个模块应该有相应的入口函数（初始化函数）提供给main.js引用注册。
- 入口函数形式【initPkg_模块名】
- 每个模块向外暴露的变量需要写好注释并放在最前面
- **新增功能的icon的svg的style必须有display:block;父元素a的class要带上ex-panel__icon**
- 例如`<a class="ex-panel__icon"><svg style="display:block;"></svg></a>`或者`<a class="ex-panel__icon"><img/></a>`
- 每个模块保存的数据名字以 ExSave_ 开头 例如ExSave_BarrageLoop
4. 编写时注意不要污染其他模块或对其他模块有所影响
5. 模块中的子模块处理方式同主模块。
- **详细可参考模仿已经编写好的模块包**

### 编译
1. 将所有package的css内容依次复制到main.js的initStyle里
2. 在main.js下的initPkg函数中依次注册所有的模块，例如`initPkg_BarrageLoop();`
3. 将package下所有模块的js代码复制到main.js下
4. 全部完成后保存，复制到油猴脚本中去。
- **可以使用文件夹中自带的编译器，编译器将依据上述规则自动生成main.js**

### 更新
1. 修改头文件里的version
2. 修改Update模块包里的version
3. 编译发布