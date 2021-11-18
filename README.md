# Ts-Vuex-Todo(整理中)

*簡略說明

1. 使用Vue-Cli建立專案，用TypeScript和Vuex來撰寫todo list app。
2. CSS使用Tailwind(安裝指令vue add tailwind)。
3. JavaScript版本的Vuex TodoList可以參考先前的作品 [Vuex-TodoList](https://github.com/Kuaruou/Vuex-TodoList)。

*設定
1. shims-vue.d.ts檔案是Ambient Declarations(外部模組定義)，給專案內的vue檔案做模組宣告，讓編輯器能辨識且使vue框架等函式庫的功能能融入TypeScript。

*Vuex
1. State: 先定義TodoItem型別裡面id, text 和 completed 屬性的基本型別，再定義State型別，裡面items的功能為儲存每個待辦事項的內容，型別為TodoItem型別的陣列。最後宣告state的原始狀態，loading為false，items為空陣列。

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

2. Mutation: 先用enum列舉且儲存MutationType裡所有的mutation。接著定義Mutations型別，將所有mutation函式中所需要的參數型別填入，且定義函式回傳值的型別，此處因皆無回傳值所以都是void型別。

```javascript
export enum MutationType {
  CreateItem = 'CREATE_ITEM',
  SetItems = 'SET_ITEMS',
  CompleteItem = 'COMPLETE_ITEM',
  SetLoading = 'SET_LOADING'
}

export type Mutations = {
  [MutationType.CreateItem](state: State, item: TodoItem): void
  [MutationType.SetItems](state: State, item: TodoItem[]): void
  [MutationType.CompleteItem](
    state: State,
    item: Partial<TodoItem> & { id: number }
  ): void
  [MutationType.SetLoading](state: State, value: boolean): void
}
```

MutationTree是vuex內建的通用型別，通用型別在定義宣告時不預先指定具體的型別，等到執行的時候才確認型別。在此處mutations以MutationTree<State> & Mutations交集型別(intersection &)來確保函式內容同時符合MutationTree<State>和Mutations型別。

```javascript
export const mutations: MutationTree<State> & Mutations = {
  [MutationType.CreateItem](state, item) {
    state.items.unshift(item)
  },
  [MutationType.SetItems](state, items) {
    state.items = items
  },
  [MutationType.CompleteItem](state, newItem) {
    const item = state.items.findIndex(s => s.id === newItem.id)
    if (item === -1) return
    state.items[item] = { ...state.items[item], ...newItem }
  },
  [MutationType.SetLoading](state, value) {
    state.loading = value
  }
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
