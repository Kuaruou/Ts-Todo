# Ts-Vuex-Todo

*整理中
*簡略說明

1. 使用Vue-Cli建立專案，用TypeScript和Vuex來撰寫todo list app。
2. CSS使用Tailwind(安裝指令vue add tailwind)。
3. JavaScript版本的Vuex TodoList可以參考先前的作品 [Vuex-TodoList](https://github.com/Kuaruou/Vuex-TodoList)。

*設定
1. shims-vue.d.ts檔案是Ambient Declarations(外部模組定義)，給專案內的vue檔案做模組宣告，讓編輯器能辨識且使vue框架等函式庫的功能能融入TypeScript。

*Vuex
1. State: 先定義TodoItem型別裡面id, text 和 completed 屬性的基本型別，再定義State型別，裡面的items為TodoItem型別的陣列，items的功能為儲存每個待辦事項的內容，最後宣告state的原始狀態。

```javascript
export type TodoItem = {
  id: number
  text: string
  completed: boolean
}

export type State = {
  loading: boolean
  items: TodoItem[]
}

export const state: State = {
  loading: false,
  items: []
}
```

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Lints and fixes files
```
npm run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
