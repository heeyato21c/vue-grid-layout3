# vue-grid-layout3

vue-grid-layout vue3 版本

## 安装

```shell
npm install vue-grid-layout-next
```

## 使用

局部注册
jsx
```typescript
import { defineComponent,ref } from 'vue'
import { GridItem, GridLayout, eventBusKey } from 'vue-grid-layout-next';
// import Bus from '@/utils/Bus';
export default defineComponent({
    name: 'App',
    setup() {
        // provide(eventBusKey, Bus); 需要外部调用方法时候使用
        const layout = ref([
            { x: 0, y: 0, w: 2, h: 2, i: '0', static: false, minH: 5 },
            { x: 2, y: 0, w: 2, h: 4, i: '1', static: true },
            { x: 4, y: 0, w: 2, h: 5, i: '2', static: false },
            { x: 6, y: 0, w: 2, h: 3, i: '3', static: false },
            { x: 8, y: 0, w: 2, h: 3, i: '4', static: false },
            { x: 10, y: 0, w: 2, h: 3, i: '5', static: false },
            { x: 0, y: 5, w: 2, h: 5, i: '6', static: false },
            { x: 2, y: 5, w: 2, h: 5, i: '7', static: false },
            { x: 4, y: 5, w: 2, h: 5, i: '8', static: false },
            { x: 6, y: 3, w: 2, h: 4, i: '9', static: true }
        ])
        return { layout }
    },
    render() {
        return (
            <GridLayout
                layout={this.layout}
                col-num={12}
                row-height={30}
                is-draggable={true}
                is-resizable={true}
                is-mirrored={false}
                vertical-compact={true}
                margin={[10, 10]}
                use-css-transforms={true}
            >
                {this.layout.map(item => (
                    <GridItem
                        key={item.i}
                        drag-allow-from='.toolbox'
                        i={item.i}
                        x={item.x}
                        y={item.y}
                        w={item.w}
                        h={item.h}
                        static={item.static}
                    >
                        <div class="box">
                            <div class="toolbox">drag</div>
                            <div class="item">
                                <div>{ item.i }</div>
                                <div>static:{ String(item.static) }</div>
                            </div>
                        </div>
                    </GridItem>
                ))}

            </GridLayout>
        )
    }
})
```

```vue
<script setup lang="ts">
import { GridItem, GridLayout } from "vue-grid-layout-next";
import type { Layout } from "vue-grid-layout-next/dist/helpers/utils";
import "v3-grid-layout/dist/style.css";
const layout: Layout = [
  { x: 0, y: 0, w: 2, h: 2, i: "0", static: false, minH: 5 },
  { x: 2, y: 0, w: 2, h: 4, i: "1", static: true },
  { x: 4, y: 0, w: 2, h: 5, i: "2", static: false },
  { x: 6, y: 0, w: 2, h: 3, i: "3", static: false },
  { x: 8, y: 0, w: 2, h: 3, i: "4", static: false },
  { x: 10, y: 0, w: 2, h: 3, i: "5", static: false },
  { x: 0, y: 5, w: 2, h: 5, i: "6", static: false },
  { x: 2, y: 5, w: 2, h: 5, i: "7", static: false },
  { x: 4, y: 5, w: 2, h: 5, i: "8", static: false },
  { x: 6, y: 3, w: 2, h: 4, i: "9", static: true },
];
</script>

<template>
  <grid-layout
    v-model:layout="layout"
    :col-num="12"
    :row-height="30"
    :is-draggable="true"
    :is-resizable="true"
    :is-mirrored="false"
    :vertical-compact="true"
    :margin="[10, 10]"
    :use-css-transforms="true"
  >
    <grid-item
      v-for="item in layout"
      :key="item.i"
      drag-allow-from=".toolbox"
      v-bind="item"
    >
      <div style="display: flex; flex-direction: column; height: 100%">
        <div
          class="toolbox"
          style="
            width: 100%;
            height: 20px;
            text-align: center;
            background-color: bisque;
          "
        >
          drag
        </div>
        <div style="height: 100%; text-align: center; background-color: #eee">
          {{ item.i }}
          <br />
          static:{{ item.static }}
        </div>
      </div>
    </grid-item>
  </grid-layout>
</template>

```