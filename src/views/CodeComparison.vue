<template>
  <section class="code-section" id="code">
    <div class="section-header">
      <span class="section-tag">实战对比</span>
      <h2 class="section-title">TodoList 完整实现</h2>
      <p class="section-subtitle">同样的功能，不同的语法</p>
    </div>
    
    <div class="code-comparison">
      <!-- 分隔线 -->
      <div class="divider" ref="divider" @mousedown="startDrag">
        <div class="divider-handle">
          <span class="handle-icon">↔</span>
        </div>
      </div>
      
      <!-- Vue 代码面板 -->
      <div class="code-panel vue-panel" :style="{ width: `${vueWidth}%` }">
        <div class="panel-header">
          <div class="panel-title">
            <span class="panel-icon vue-icon">
              <svg viewBox="0 0 24 24" fill="currentColor">
                <path d="M2 3h3.5L12 14.75 18.5 3H22L12 21 2 3m6.5 0H12l6.5 11.25V3H15v3.75L12 9.75 9 6.75V3H6.5v3.75L2 3h4.5z"/>
              </svg>
            </span>
            <span>Vue3 + TypeScript</span>
          </div>
          <span class="file-name">TodoList.vue</span>
        </div>
        <div class="code-content">
          <pre class="code-block vue"><code><span class="line-number" v-for="n in 35" :key="n">{{ n }}</span><span class="code-text">{{ vueCode }}</span></code></pre>
        </div>
      </div>
      
      <!-- Harmony 代码面板 -->
      <div class="code-panel harmony-panel" :style="{ width: `${100 - vueWidth}%` }">
        <div class="panel-header">
          <div class="panel-title">
            <span class="panel-icon harmony-icon">H</span>
            <span>HarmonyOS ArkTS</span>
          </div>
          <span class="file-name">TodoList.ets</span>
        </div>
        <div class="code-content">
          <pre class="code-block harmony"><code><span class="line-number" v-for="n in 35" :key="n">{{ n }}</span><span class="code-text">{{ harmonyCode }}</span></code></pre>
        </div>
      </div>
    </div>
    
    <!-- 功能对比标签 -->
    <div class="feature-tags">
      <div class="feature-tag" v-for="(feature, index) in features" :key="index"
           :style="{ animationDelay: `${index * 0.1}s` }">
        <span class="tag-check">✓</span>
        <span>{{ feature }}</span>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
import { ref, onUnmounted } from 'vue'

const vueWidth = ref(50)
const divider = ref<HTMLElement | null>(null)
const isDragging = ref(false)

const vueCode = `<template>
  <div class="todo-container">
    <h2>待办事项</h2>
    
    <div class="input-area">
      <input 
        v-model="newTodo" 
        @keyup.enter="addTodo"
        placeholder="输入新任务..."
      />
      <button @click="addTodo">添加</button>
    </div>
    
    <ul class="todo-list">
      <li 
        v-for="todo in filteredTodos" 
        :key="todo.id"
        :class="{ completed: todo.completed }"
      >
        <input 
          type="checkbox" 
          v-model="todo.completed"
        />
        <span>{{ todo.text }}</span>
        <button @click="deleteTodo(todo.id)">删除</button>
      </li>
    </ul>
    
    <div class="footer">
      <span>{{ remaining }} 项未完成</span>
      <div class="filters">
        <button 
          v-for="filter in filters" 
          :key="filter"
          :class="{ active: currentFilter === filter }"
          @click="currentFilter = filter"
        >
          {{ filter }}
        </button>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, computed } from 'vue'

interface Todo {
  id: number
  text: string
  completed: boolean
}

const newTodo = ref('')
const todos = ref<Todo[]>([])
const currentFilter = ref('全部')
const filters = ['全部', '进行中', '已完成']

const filteredTodos = computed(() => {
  switch (currentFilter.value) {
    case '进行中':
      return todos.value.filter(t => !t.completed)
    case '已完成':
      return todos.value.filter(t => t.completed)
    default:
      return todos.value
  }
})

const remaining = computed(() => {
  return todos.value.filter(t => !t.completed).length
})

let nextId = 1
const addTodo = () => {
  if (!newTodo.value.trim()) return
  todos.value.push({
    id: nextId++,
    text: newTodo.value,
    completed: false
  })
  newTodo.value = ''
}

const deleteTodo = (id: number) => {
  const index = todos.value.findIndex(t => t.id === id)
  if (index > -1) {
    todos.value.splice(index, 1)
  }
}
<\/script>`

const harmonyCode = `interface Todo {
  id: number
  text: string
  completed: boolean
}

type FilterType = '全部' | '进行中' | '已完成'

@Entry
@Component
struct TodoList {
  @State newTodo: string = ''
  @State todos: Todo[] = []
  @State currentFilter: FilterType = '全部'
  
  private filters: FilterType[] = ['全部', '进行中', '已完成']
  private nextId: number = 1
  
  @Computed get filteredTodos(): Todo[] {
    switch (this.currentFilter) {
      case '进行中':
        return this.todos.filter(t => !t.completed)
      case '已完成':
        return this.todos.filter(t => t.completed)
      default:
        return this.todos
    }
  }
  
  @Computed get remaining(): number {
    return this.todos.filter(t => !t.completed).length
  }
  
  addTodo() {
    if (!this.newTodo.trim()) return
    this.todos.push({
      id: this.nextId++,
      text: this.newTodo,
      completed: false
    })
    this.newTodo = ''
  }
  
  deleteTodo(id: number) {
    const index = this.todos.findIndex(t => t.id === id)
    if (index > -1) {
      this.todos.splice(index, 1)
    }
  }
  
  build() {
    Column({ space: 20 }) {
      Text('待办事项').fontSize(28).fontWeight(FontWeight.Bold)
      
      Row({ space: 10 }) {
        TextInput({ placeholder: '输入新任务...', text: $$this.newTodo })
          .layoutWeight(1)
        Button('添加').onClick(() => this.addTodo())
      }
      
      List({ space: 10 }) {
        ForEach(this.filteredTodos, (todo: Todo) => {
          ListItem() {
            Row({ space: 10 }) {
              Checkbox().select(todo.completed)
              Text(todo.text).layoutWeight(1)
              Button('删除').onClick(() => this.deleteTodo(todo.id))
            }
          }
        })
      }
      
      Row() {
        Text(\`\${this.remaining} 项未完成\`)
        Row({ space: 5 }) {
          ForEach(this.filters, (filter: FilterType) => {
            Button(filter).onClick(() => {
              this.currentFilter = filter
            })
          })
        }
      }
    }
    .padding(20)
  }
}`

const features = [
  '响应式状态管理',
  '计算属性',
  '列表渲染',
  '事件处理',
  '条件渲染',
  '双向绑定'
]

const startDrag = (_e: MouseEvent) => {
  isDragging.value = true
  document.addEventListener('mousemove', handleDrag)
  document.addEventListener('mouseup', stopDrag)
}

const handleDrag = (e: MouseEvent) => {
  if (!isDragging.value) return
  const container = divider.value?.parentElement
  if (!container) return
  
  const rect = container.getBoundingClientRect()
  const percentage = ((e.clientX - rect.left) / rect.width) * 100
  vueWidth.value = Math.max(30, Math.min(70, percentage))
}

const stopDrag = () => {
  isDragging.value = false
  document.removeEventListener('mousemove', handleDrag)
  document.removeEventListener('mouseup', stopDrag)
}

onUnmounted(() => {
  document.removeEventListener('mousemove', handleDrag)
  document.removeEventListener('mouseup', stopDrag)
})
</script>

<style scoped>
.code-section {
  padding: 120px 40px;
  position: relative;
}

.section-header {
  text-align: center;
  margin-bottom: 60px;
}

.section-tag {
  display: inline-block;
  padding: 8px 20px;
  background: rgba(254, 131, 1, 0.1);
  border: 1px solid rgba(254, 131, 1, 0.3);
  border-radius: 50px;
  font-size: 0.85rem;
  font-weight: 600;
  color: var(--primary);
  margin-bottom: 20px;
}

.section-title {
  font-size: clamp(2.5rem, 5vw, 4rem);
  font-weight: 800;
  margin-bottom: 16px;
  color: var(--title);
}

.section-subtitle {
  font-size: 1.2rem;
  color: var(--body);
  opacity: 0.7;
}

/* 代码对比区域 */
.code-comparison {
  max-width: 1400px;
  margin: 0 auto;
  display: flex;
  height: 600px;
  border-radius: 24px;
  overflow: hidden;
  box-shadow: 0 30px 60px rgba(0, 0, 0, 0.15);
  position: relative;
}

.code-panel {
  height: 100%;
  overflow: hidden;
  transition: width 0.1s ease-out;
}

.vue-panel {
  background: #1a1a2e;
}

.harmony-panel {
  background: #0d1b2a;
}

.panel-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 16px 24px;
  border-bottom: 1px solid rgba(255, 255, 255, 0.1);
}

.panel-title {
  display: flex;
  align-items: center;
  gap: 12px;
  color: white;
  font-weight: 600;
  font-size: 0.95rem;
}

.panel-icon {
  width: 28px;
  height: 28px;
  border-radius: 6px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.vue-icon {
  background: rgba(66, 184, 131, 0.2);
  color: #42b883;
}

.vue-icon svg {
  width: 18px;
  height: 18px;
}

.harmony-icon {
  background: rgba(254, 131, 1, 0.2);
  color: #fe8301;
  font-weight: 700;
  font-size: 0.85rem;
}

.file-name {
  color: rgba(255, 255, 255, 0.5);
  font-size: 0.85rem;
  font-family: 'Fira Code', monospace;
}

.code-content {
  height: calc(100% - 60px);
  overflow: auto;
  padding: 20px 0;
}

.code-block {
  margin: 0;
  padding: 0 24px;
  font-family: 'Fira Code', monospace;
  font-size: 0.8rem;
  line-height: 1.8;
  white-space: pre;
  position: relative;
}

.line-number {
  display: inline-block;
  width: 30px;
  color: rgba(255, 255, 255, 0.3);
  text-align: right;
  margin-right: 16px;
  user-select: none;
}

.code-text {
  color: #e6edf3;
}

/* 代码高亮 */
.vue-panel .code-text {
  color: #a5d6ff;
}

.vue-panel .code-text :deep(.keyword) {
  color: #ff7b72;
}

.harmony-panel .code-text {
  color: #ffa657;
}

/* 分隔线 */
.divider {
  position: absolute;
  top: 0;
  left: 50%;
  transform: translateX(-50%);
  width: 4px;
  height: 100%;
  background: linear-gradient(180deg, transparent, rgba(254, 131, 1, 0.5), transparent);
  cursor: col-resize;
  z-index: 10;
  transition: background 0.3s ease;
}

.divider:hover {
  background: linear-gradient(180deg, transparent, rgba(254, 131, 1, 0.8), transparent);
}

.divider-handle {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 40px;
  height: 40px;
  background: var(--primary);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow: 0 4px 20px rgba(254, 131, 1, 0.4);
  transition: transform 0.3s cubic-bezier(0.68, -0.6, 0.32, 1.6);
}

.divider:hover .divider-handle {
  transform: translate(-50%, -50%) scale(1.1);
}

.handle-icon {
  color: white;
  font-size: 1.2rem;
  font-weight: bold;
}

/* 功能标签 */
.feature-tags {
  max-width: 1400px;
  margin: 40px auto 0;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  gap: 16px;
}

.feature-tag {
  display: flex;
  align-items: center;
  gap: 8px;
  padding: 10px 20px;
  background: white;
  border-radius: 50px;
  font-size: 0.9rem;
  font-weight: 600;
  color: var(--body);
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.08);
  animation: slideInUp 0.6s ease-out forwards;
  opacity: 0;
}

.tag-check {
  width: 20px;
  height: 20px;
  background: linear-gradient(135deg, #42b883 0%, #fe8301 100%);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  color: white;
  font-size: 0.7rem;
}

/* 响应式 */
@media (max-width: 1024px) {
  .code-comparison {
    flex-direction: column;
    height: auto;
  }
  
  .code-panel {
    width: 100% !important;
    height: 400px;
  }
  
  .divider {
    display: none;
  }
}

@media (max-width: 768px) {
  .code-section {
    padding: 80px 20px;
  }
  
  .code-panel {
    height: 300px;
  }
  
  .code-block {
    font-size: 0.7rem;
  }
}
</style>