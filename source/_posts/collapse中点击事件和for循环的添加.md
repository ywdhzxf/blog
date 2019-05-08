
---
title: collapse中点击事件和for循环的添加
date: 2019-05-06 12:36:15
tags: web前端
---


###  因为有些样式要用手风琴效果,然后代码写上之后发现 el-collapse-item里面不能用点击事件,我的代码本来是

```
     <el-collapse   :data="menuList" v-for="(menu,index) in menuList"  accordion>
        <el-collapse-item :title="menu.field"  @click="details_list(index,menuList)" :name="index" >
          <div >
            <el-table :data="details_lis" element-loading-text="给我一点时间" border fit highlight-current-row style="width: 100%">
              <el-table-column align="center" label="字段" min-width="100%">
                <template scope="scope">
                  <span>{{ scope.row.key }}</span>
                </template>
              </el-table-column>
              <el-table-column align="center" label="参数" min-width="100%">
                <template scope="scope">
                  <span>{{  scope.row.value }}</span>
                </template>
              </el-table-column>
            </el-table>
          </div>
        </el-collapse-item>
        </el-collapse>
```
哇,怎么试都不行,不停在调位置,然后最后参考了一个segmentfault的多级嵌套的点击事件,发现他的点击事件都是在div标签中写的,于是问题解决,代码如下

```
<el-collapse   :data="menuList"  accordion>
        <div v-for="(menu,index) in menuList" @click="details_list(index,menuList)">
        <el-collapse-item :title="menu.field"   :name="index" >
          <div >
            <el-table :data="details_lis" element-loading-text="给我一点时间" border fit highlight-current-row style="width: 100%">
              <el-table-column align="center" label="字段" min-width="100%">
                <template scope="scope">
                  <span>{{ scope.row.key }}</span>
                </template>
              </el-table-column>
              <el-table-column align="center" label="参数" min-width="100%">
                <template scope="scope">
                  <span>{{  scope.row.value }}</span>
                </template>
              </el-table-column>
            </el-table>
          </div>
        </el-collapse-item>
        </div>
        </el-collapse>
```

    