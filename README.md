# ztreev(vue2.x组件)
环境是抄的这个哥们的[项目](https://github.com/Litor/ztree-vue)的，npm安装他的包不能用,因为他是1.0版本，自己搞支持vue2.x版本。
目前是一个纯粹的包裹一下，没有任何改动。

[![NPM](https://nodei.co/npm/ztreev.png)](https://nodei.co/npm/ztreev/)

### 例子
1. 我使用的是vue-cli初始化的项目
`vue init webpack PROJECT_NAME`

2. webpack.base.conf.js添加配置,否则找不到jQuery、$、_ 等变量。
    ```
    plugins: [
      new webpack.ProvidePlugin({
        jQuery: 'jquery',
        $: 'jquery',
        _: 'lodash'
      })
    ]
    ```
3. vue代码
    ```vue
    //加载静态数据
    <template>
      <ztree
        :setting="{
          async:{
            url: './data.json'
          },
          data: {
            key: {
                name: 'label'
            }
          }
        }"
        :data="[
        {
          label: '父节点1 - 展开',
          open: true,
          children: [
            {
              label: '父节点11 - 折叠',
              children: [
                {
                  label: '叶子节点111'
                },
                {
                  label: '叶子节点112'
                },
                {
                  label: '叶子节点113'
                },
                {
                  label: '叶子节点114'
                }
              ]
            },
            {
              label: '父节点12 - 折叠',
              children: [
                {
                  label: '叶子节点121'
                },
                {
                  label: '叶子节点122'
                },
                {
                  label: '叶子节点123'
                },
                {
                  label: '叶子节点124'
                }
              ]
            },
            {
              label: '父节点13 - 没有子节点',
              isParent: true
            }
          ]
        }
      ]"
      >
      </ztree>
    </template>
    <style>
      @import "~ztree/css/metroStyle/metroStyle.css";
    </style>
    ```
    ```vue
    //异步加载数据
    <template>
      <ztree :setting="{
        data:{
          key:{
            name:'label'
          }
        },
        once:{
          url: './static/data/tree.json',
          type : 'GET',
          data :{param:123},
          dataFilter:function(data){
            return data
          }
        }
      }"></ztree>
    </template>
    
    <style>
      @import "~ztree/css/metroStyle/metroStyle.css";
    </style>

    ```
### Attributes
| 参数      | 说明          | 类型      | 默认值                           |  备注 |
|---------- |-------------- |---------- |--------------------------------  |-------- |
| setting     | ztree origin setting | Object    |— | 参考 http://www.treejs.cn/v3/api.php<br/>加了一个once[Object]属性,一次加载所有树形数据，配置同$.ajax()的option<br/>但是其中的dataFilter方法是在ajax回调里执行的。   |
| data     | localdata | Array    | —                               | 静态数据[Array]    |

可以给组件绑定事件，目前只支持`vm.$on`这种方法给树添加事件钩子，与ztree一致。
回调的最后一个参数用于存储返回值，比如
```js
comp.$on('beforeDrop',function(treeId, treeNodes, targetNode, moveType, isCopy, store){
  store.cancel = true // 防止拖放完成
})
```

### API
|  方法  |  参数  |  说明  |
|-------|------|--------|
|action  |   actionName(方法名),args...(方法参数)   | 调用treeObj的方法，如comp.action('getNodeByTId','123')<br/>comp.action('getNodesByFilter',filter, isSingle, parentNode, invokeParam) |
|refresh |mergeSetting(需要覆盖的配置)|与原setting混合，完成修改setting的效果，并重新初始化ztree.<br/>使用场景：开始时tree没有checkbox，调用<br/>comp.refresh({check:{enable:true}})给tree增加checkbox
