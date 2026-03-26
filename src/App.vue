<script setup lang="ts">
import { ref, computed } from 'vue'

const activeTab = ref<'general' | 'tailwind'>('general')
const activeGenreId = ref('action')

const generalGenres = [
  {
    id: 'action',
    name: 'Action & Trigger',
    description: '処理を実行したり、画面を切り替えたりするためのパーツ。',
    parts: [
      {
        name: "Primary Button (主要ボタン)",
        description: "画面内で最も重要な操作を促すボタン。視覚的に最も目立たせる必要がある。",
        prompt: "「ホバー時に背景がわずかに明るいグレーになり、アクティブ時にスケールダウンするアニメーションを持つ、角丸の完全にべた塗り（Solid）のPrimaryボタンを作成してください。色はパールホワイト（stone-100）で、文字は黒（neutral-900）にしてください。」",
        demoComponent: "primary-button"
      },
      {
        name: "Secondary Button (副次ボタン)",
        description: "キャンセルのような副次的な操作。Primaryボタンの邪魔にならないよう、アウトラインやゴーストスタイルが使われる。",
        prompt: "「背景は透明で、細いボーダー（neutral-700）を持つOutlineボタンを作成してください。ホバー時に入力エリアと同じように背景色がわずかに明るいグレー（neutral-800）になるように指定してください。」",
        demoComponent: "secondary-button"
      },
      {
        name: "Icon Button (アイコンボタン)",
        description: "テキストを用いず、アイコンのみで機能を示すコンパクトなボタンコンポーネント。",
        prompt: "「正方形から角丸（rounded-lg）にし、中央にSVGアイコンを配置したアイコンボタンを作成してください。ホバー時に丸い灰色の背景（bg-neutral-800）がフェードインするような心地よいインタラクションを与えてください。」",
        demoComponent: "icon-button"
      },
      {
        name: "Dropdown Menu (ドロップダウン)",
        description: "クリック時に展開されるアクションのリスト。多数のアクションをスッキリとまとめる。",
        prompt: "「ボタン押下で下部にフロートするドロップダウンメニューを作成してください。メニュー本体は背景暗めのグレー（neutral-800/90）、うっすらとしたボーダー（neutral-700）、ドロップシャドウを付け、各アイテムはホバーで色が変わるように設計してください。」",
        demoComponent: "dropdown"
      },
      {
        name: "Floating Action Button (FAB)",
        description: "画面の右下などに常に固定表示される特別な主要アクションボタン。",
        prompt: "「画面の右下に絶対配置（fixed）された円形のシャドウ付きボタンを作成してください。色は白（bg-white）で、スクロールしても常に手前（z-50）に被さるようにし、ホバー時にはフワッと少し浮き上がる（-translate-y-1）ようにしてください。」",
        demoComponent: "fab"
      }
    ]
  },
  {
    id: 'input',
    name: 'Input & Forms',
    description: 'ユーザーからの情報を受け取るためのパーツ。(準備中)',
    parts: []
  },
  {
    id: 'navigation',
    name: 'Navigation',
    description: 'ユーザーが目的地に辿り着くためのパーツ。(準備中)',
    parts: []
  },
  {
    id: 'container',
    name: 'Container & Layout',
    description: '情報をグループ化する器のパーツ。(準備中)',
    parts: []
  },
  {
    id: 'feedback',
    name: 'Status & Feedback',
    description: 'システムの状態を画面上に返すパーツ。(準備中)',
    parts: []
  }
]

const activeGenre = computed(() => generalGenres.find(g => g.id === activeGenreId.value))

const tailwindParts = [
  {
    name: "Glass (グラス)",
    description: "背景がすりガラスのように透けて見える、モダンで上質なUI表現。",
    prompt: "「Tailwindの `bg-neutral-800/40 backdrop-blur-lg border border-neutral-700/50` のようなクラスを使用して、背景が上品に透けるグラスモーフィズムのコンテナを作成してください。」",
    demoComponent: "glass"
  },
  {
    name: "Gradient Text (グラデーション)",
    description: "文字色にソフトなグラデーションを適用し、上質な見出しを作るテクニック。",
    prompt: "「テキストに `text-transparent bg-clip-text bg-linear-to-br from-neutral-200 to-neutral-500` を適用し、美しいグラデーションのタイポグラフィを作成してください。」",
    demoComponent: "gradientText"
  },
  {
    name: "Soft Glow (ソフトグロー)",
    description: "要素の周囲に控えめな影を落とし、柔らかく光を浴びているように見せる表現。",
    prompt: "「ボタンのホバー時に、`shadow-md shadow-white/5` などのクラスを使用して、要素が柔らかい光を放っているような控えめなグローエフェクトを追加してください。」",
    demoComponent: "glow"
  },
  {
    name: "Skeleton (スケルトン)",
    description: "データ読み込み中に、要素の形だけを静かに表示するローディングUI。",
    prompt: "「`animate-pulse` クラスと `bg-neutral-800` を組み合わせた丸みのあるブロック配置し、読み込み中を示すミニマルなスケルトンUIを作成してください。」",
    demoComponent: "skeleton"
  }
]
</script>

<template>
  <div class="min-h-screen bg-neutral-900 text-stone-300 flex flex-col items-center selection:bg-stone-100/10 font-sans">
    <header class="w-full max-w-6xl px-8 py-16">
      <div class="inline-flex items-center gap-3 mb-6">
        <div class="w-10 h-[1px] bg-neutral-700"></div>
        <span class="text-xs font-bold text-neutral-500 tracking-[0.2em] uppercase">VibeCoding UI</span>
      </div>
      <h1 class="text-5xl md:text-7xl font-extrabold tracking-tight text-white mb-8 leading-[1.1]">
        UI Dictionary<br />
        <span class="text-neutral-600">for AI Assistants</span>
      </h1>
      <p class="text-neutral-500 text-xl max-w-2xl leading-relaxed">
        温もりを感じるグレーと、鮮明なパールホワイト。AIと共創するための洗練されたUIリファレンス。
      </p>
    </header>

    <main class="w-full max-w-6xl px-8 pb-32 flex-1">
      <!-- Top level Tabs -->
      <nav class="flex flex-wrap items-center gap-8 md:gap-12 border-b border-neutral-800 mb-12">
        <button
          @click="activeTab = 'general'"
          :class="[
            'pb-6 text-sm md:text-base font-bold tracking-wider transition-all duration-300 border-b-2 whitespace-nowrap',
            activeTab === 'general' ? 'border-white text-white' : 'border-transparent text-neutral-600 hover:text-neutral-400'
          ]"
        >
          General Components
        </button>
        <button
          @click="activeTab = 'tailwind'"
          :class="[
            'pb-6 text-sm md:text-base font-bold tracking-wider transition-all duration-300 border-b-2 whitespace-nowrap',
            activeTab === 'tailwind' ? 'border-white text-white' : 'border-transparent text-neutral-600 hover:text-neutral-400'
          ]"
        >
          Tailwind Patterns
        </button>
      </nav>

      <!-- Tab Contents -->
      <div class="relative min-h-[600px]">
        <Transition name="page" mode="out-in">
          
          <!-- General Tab Layout (Sidebar + Content) -->
          <div v-if="activeTab === 'general'" key="general" class="flex flex-col md:flex-row gap-12">
            
            <!-- Sidebar: Genres -->
            <aside class="w-full md:w-64 shrink-0 flex flex-col gap-2 border-l border-neutral-800 pl-6">
              <h3 class="text-[10px] font-black uppercase tracking-[0.2em] text-neutral-500 mb-4 pl-4 pt-2">Component Genres</h3>
              <button
                v-for="genre in generalGenres"
                :key="genre.id"
                @click="activeGenreId = genre.id"
                class="text-left px-4 py-3 rounded-lg text-sm font-semibold transition-all relative group"
                :class="activeGenreId === genre.id ? 'text-white bg-neutral-800/50' : 'text-neutral-500 hover:text-stone-300 hover:bg-neutral-800/30'"
              >
                <!-- Active Indicator indicator -->
                <div v-if="activeGenreId === genre.id" class="absolute left-[-24px] top-1/2 -translate-y-1/2 w-1.5 h-6 bg-white rounded-r-md"></div>
                {{ genre.name }}
              </button>
            </aside>

            <!-- Main Content Area: Genre Parts -->
            <div class="flex-1" v-if="activeGenre">
              <div class="mb-12">
                <h2 class="text-3xl font-extrabold text-white mb-4">{{ activeGenre.name }}</h2>
                <p class="text-neutral-400 text-lg">{{ activeGenre.description }}</p>
                <div v-if="activeGenre.parts.length === 0" class="mt-8 p-12 border border-dashed border-neutral-700/50 rounded-2xl flex items-center justify-center text-neutral-500 text-sm italic">
                  準備中 (Coming Soon)
                </div>
              </div>

              <!-- Grid of UI Parts in the Genre -->
              <div v-if="activeGenre.parts.length > 0" class="grid grid-cols-1 md:grid-cols-2 gap-10">
                <div v-for="(item, index) in activeGenre.parts" :key="index" class="group flex flex-col h-full">
                  <!-- Demo Area -->
                  <div class="aspect-video bg-neutral-900 border border-neutral-800 rounded-2xl mb-6 flex flex-col items-center justify-center relative overflow-hidden transition-all duration-500 group-hover:border-neutral-700 group-hover:bg-[#1E1E1E]">
                    
                    <template v-if="item.demoComponent === 'primary-button'">
                      <button class="px-8 py-3 bg-stone-100 text-neutral-900 font-bold rounded-full transition-all hover:bg-white active:scale-95 shadow-lg shadow-white/5">
                        Primary Action
                      </button>
                    </template>
                    
                    <template v-else-if="item.demoComponent === 'secondary-button'">
                      <button class="px-8 py-3 bg-transparent text-stone-300 font-bold rounded-full border border-neutral-700 transition-all hover:bg-neutral-800 active:scale-95">
                        Secondary Action
                      </button>
                    </template>

                    <template v-else-if="item.demoComponent === 'icon-button'">
                      <button class="w-12 h-12 flex items-center justify-center bg-transparent rounded-lg border border-transparent text-stone-400 transition-all hover:bg-neutral-800 hover:text-stone-100 active:scale-95">
                        <svg xmlns="http://www.w3.org/2000/svg" class="w-6 h-6" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><rect x="3" y="3" width="18" height="18" rx="2" ry="2"></rect><circle cx="8.5" cy="8.5" r="1.5"></circle><polyline points="21 15 16 10 5 21"></polyline></svg>
                      </button>
                    </template>
                    
                    <template v-else-if="item.demoComponent === 'dropdown'">
                      <div class="relative inline-block text-left w-48 mt-12">
                        <div class="absolute inset-x-0 bottom-4 origin-bottom bg-neutral-800 border border-neutral-700 rounded-xl shadow-2xl p-1 z-10">
                          <div class="px-3 py-2 text-sm text-stone-200 hover:bg-neutral-700/50 rounded-lg cursor-pointer transition-colors">Edit properties</div>
                          <div class="px-3 py-2 text-sm text-stone-200 hover:bg-neutral-700/50 rounded-lg cursor-pointer transition-colors">Duplicate</div>
                          <div class="my-1 h-[1px] bg-neutral-700"></div>
                          <div class="px-3 py-2 text-sm text-red-400 hover:bg-red-400/10 rounded-lg cursor-pointer transition-colors">Move to trash</div>
                        </div>
                      </div>
                    </template>

                    <template v-else-if="item.demoComponent === 'fab'">
                      <div class="absolute bottom-6 right-6 w-14 h-14 bg-stone-100 text-neutral-900 rounded-full flex items-center justify-center shadow-xl shadow-white/10 cursor-pointer transition-all hover:-translate-y-1 hover:shadow-white/20 active:scale-95">
                        <svg xmlns="http://www.w3.org/2000/svg" class="w-6 h-6" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><line x1="12" y1="5" x2="12" y2="19"></line><line x1="5" y1="12" x2="19" y2="12"></line></svg>
                      </div>
                    </template>
                  </div>

                  <!-- Text Content -->
                  <div class="flex-1 flex flex-col">
                    <h3 class="text-xl font-bold mb-3">{{ item.name }}</h3>
                    <p class="text-neutral-500 text-sm leading-relaxed mb-6">{{ item.description }}</p>
                    
                    <div class="bg-neutral-800/80 p-5 rounded-2xl border-l-4 border-neutral-600 transition-all group-hover:bg-neutral-800 group-hover:border-stone-400 mt-auto">
                      <div class="text-[10px] font-black uppercase tracking-[0.2em] text-neutral-400 mb-3">Effective Prompting</div>
                      <p class="text-stone-300 text-sm leading-relaxed italic font-medium">
                        {{ item.prompt }}
                      </p>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>

          <!-- Tailwind Tab -->
          <div v-else-if="activeTab === 'tailwind'" key="tailwind" class="grid grid-cols-1 md:grid-cols-3 gap-10">
            <div v-for="(item, index) in tailwindParts" :key="index" class="group flex flex-col h-full">
              <!-- Demo Area -->
              <div class="aspect-video bg-neutral-900 border border-neutral-800 rounded-2xl mb-6 flex flex-col items-center justify-center relative overflow-hidden transition-all duration-500 group-hover:border-neutral-700 group-hover:bg-[#1E1E1E]">
                
                <template v-if="item.demoComponent === 'glass'">
                  <div class="absolute inset-x-0 top-0 h-1/2 bg-neutral-700/50"></div>
                  <div class="w-2/3 h-1/2 bg-neutral-100/5 backdrop-blur-xl border border-white/10 p-4 rounded-2xl shadow-2xl relative">
                    <div class="h-4 w-1/3 bg-white/20 rounded"></div>
                  </div>
                </template>
                
                <template v-else-if="item.demoComponent === 'gradientText'">
                  <h2 class="text-3xl font-black text-transparent bg-clip-text bg-linear-to-br from-neutral-200 to-neutral-600">
                    Sophisticated
                  </h2>
                </template>

                <template v-else-if="item.demoComponent === 'glow'">
                  <div class="px-6 py-3 bg-neutral-800 border border-neutral-700 text-stone-100 font-bold rounded-xl shadow-[0_0_20px_rgba(255,255,255,0.05)] transition-all">
                    Subtle Glow
                  </div>
                </template>

                <template v-else-if="item.demoComponent === 'skeleton'">
                  <div class="w-3/4 flex gap-4">
                    <div class="w-10 h-10 rounded-full bg-neutral-800 animate-pulse"></div>
                    <div class="flex-1 space-y-2">
                      <div class="h-3 bg-neutral-800 rounded-full animate-pulse w-3/4"></div>
                      <div class="h-2 bg-neutral-800 rounded-full animate-pulse w-1/2"></div>
                    </div>
                  </div>
                </template>
              </div>

              <!-- Text Content -->
              <div class="flex-1 flex flex-col">
                <h3 class="text-xl font-bold mb-3">{{ item.name }}</h3>
                <p class="text-neutral-500 text-sm leading-relaxed mb-6">{{ item.description }}</p>
                
                <div class="bg-neutral-800/80 p-5 rounded-2xl border-l-4 border-neutral-600 transition-all group-hover:bg-neutral-800 group-hover:border-stone-400 mt-auto">
                  <div class="text-[10px] font-black uppercase tracking-[0.2em] text-neutral-400 mb-3">Tailwind Instruction</div>
                  <p class="text-stone-300 text-sm leading-relaxed italic font-medium">
                    {{ item.prompt }}
                  </p>
                </div>
              </div>
            </div>
          </div>
        </Transition>
      </div>
    </main>

    <footer class="w-full max-w-6xl px-8 py-16 border-t border-neutral-800 text-xs font-bold tracking-widest text-neutral-600 uppercase flex flex-col md:flex-row gap-4 justify-between items-center">
      <span>VibeCoding Encyclopedia</span>
      <span>&copy; 2026</span>
    </footer>
  </div>
</template>

<style scoped>
.page-enter-active,
.page-leave-active {
  transition: opacity 0.4s cubic-bezier(0.23, 1, 0.32, 1), transform 0.4s cubic-bezier(0.23, 1, 0.32, 1);
}
.page-enter-from {
  opacity: 0;
  transform: translateY(15px);
}
.page-leave-to {
  opacity: 0;
  transform: translateY(-15px);
}
</style>
