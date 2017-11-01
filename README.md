# ztreev(vue2.x组件)
环境是抄的这个哥们的[项目](https://github.com/Litor/ztree-vue)的，npm安装他的包不能用,因为他是1.0版本，自己搞支持vue2.x版本。

[![NPM](https://nodei.co/npm/ztreev.png)](https://nodei.co/npm/ztreev/)

### 例子
1. 我使用的是vue-cli初始化的项目
`vue init webpack PROJECT_NAME`

2. webpack.base.conf.js添加配置,否则找不到jQuery、$、_、Vue等变量。
    ```
    plugins: [
      new webpack.ProvidePlugin({
        jQuery: 'jquery',
        $: 'jquery',
        _: 'lodash',
        Vue: 'vue'
      })
    ]
    ```
3. vue代码
    ```vue
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
        },
        {
          label: '父节点2 - 折叠',
          children: [
            {
              label: '父节点21 - 展开',
              open: true,
              children: [
                {
                  label: '叶子节点211'
                },
                {
                  label: '叶子节点212'
                },
                {
                  label: '叶子节点213'
                },
                {
                  label: '叶子节点214'
                }
              ]
            },
            {
              label: '父节点22 - 折叠',
              children: [
                {
                  label: '叶子节点221'
                },
                {
                  label: '叶子节点222'
                },
                {
                  label: '叶子节点223'
                },
                {
                  label: '叶子节点224'
                }
              ]
            }
          ]
        }
      ]"
      >
      </ztree>
    </template>
    //引入你需要的样式
    <style>
      @import "~ztree/css/metroStyle/metroStyle.css";
    </style>
    ```
