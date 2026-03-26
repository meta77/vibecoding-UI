<script setup lang="ts">
import { ref, computed } from 'vue'

const activeTab = ref<'general' | 'tailwind'>('general')
const activeGenreId = ref('action')

const generalGenres = [
  {
    id: 'action',
    name: 'Action & Trigger',
    description: 'ユーザーのアクションを誘発し、処理を実行するためのコンポーネント。',
    parts: [
      {
        name: "Primary Button (主要ボタン)",
        description: "画面内で最も重要な操作を促すボタン。視覚的に最も目立たせる必要がある。コンテキストに応じた「次へ」「保存」「送信」などのアクションに使用。",
        prompt: "「ホバー時に背景がわずかに明るいグレーになり、アクティブ時にスケールダウンするアニメーションを持つ、角丸の完全にべた塗り（Solid）のPrimaryボタンを作成してください。色はパールホワイト（stone-100）で、文字は黒（neutral-900）にしてください。」",
        demoComponent: "primary-button"
      },
      {
        name: "Secondary Button (副次ボタン)",
        description: "キャンセルのような副次的な操作。Primaryボタンの視覚的な重みを邪魔しないよう、アウトラインやゴーストスタイルが選ばれることが多い。",
        prompt: "「背景は透明で、細いボーダー（neutral-700）を持つOutlineボタンを作成してください。ホバー時に入力エリアと同じように背景色がわずかに明るいグレー（neutral-800）になるように指定してください。」",
        demoComponent: "secondary-button"
      },
      {
        name: "Icon Button (アイコンボタン)",
        description: "テキストを用いず、アイコンのみで機能を示す。ツールバーやナビゲーション内の省スペースなアクションに最適。",
        prompt: "「正方形から角丸（rounded-lg）にし、中央にSVGアイコンを配置したアイコンボタンを作成してください。ホバー時に丸い灰色の背景（bg-neutral-800）がフェードインするような心地よいインタラクションを与えてください。」",
        demoComponent: "icon-button"
      },
      {
        name: "Dropdown Menu (ドロップダウン)",
        description: "クリック時に展開されるアクションのリスト。設定、プロファイル、多機能なアクションをスッキリとまとめる。",
        prompt: "「ボタン押下で下部にフロートするドロップダウンメニューを作成してください。メニュー本体は背景暗めのグレー（neutral-800/90）、うっすらとしたボーダー（neutral-700）、ドロップシャドウを付け、各アイテムはホバーで色が変わるように設計してください。」",
        demoComponent: "dropdown"
      },
      {
        name: "Floating Action Button (FAB)",
        description: "画面の右下などに常に固定表示される特別なアクション。モバイルや一覧性の高い画面での「新規作成」などに使われる。",
        prompt: "「画面の右下に絶対配置（fixed）された円形のシャドウ付きボタンを作成してください。色は白（bg-white）で、スクロールしても常に手前（z-50）に被さるようにし、ホバー時にはフワッと少し浮き上がる（-translate-y-1）ようにしてください。」",
        demoComponent: "fab"
      }
    ]
  },
  { id: 'input', name: 'Input & Forms', description: 'ユーザーからの情報を受け取るためのパーツ。(準備中)', parts: [] },
  { id: 'navigation', name: 'Navigation', description: '目的地に辿り着くためのパーツ。(準備中)', parts: [] },
  { id: 'container', name: 'Container & Layout', description: '情報をグループ化する器のパーツ。(準備中)', parts: [] },
  { id: 'feedback', name: 'Status & Feedback', description: 'システムの状態を画面上に返すパーツ。(準備中)', parts: [] }
]

const activeGenre = computed(() => generalGenres.find(g => g.id === activeGenreId.value))

const tailwindParts = [
  {
    name: "Glass (グラス)",
    description: "背景がすりガラスのように透けて見える、モダンで上質なUI表現。北欧風の清潔感あるデザインに最適。",
    prompt: "「Tailwindの `bg-neutral-800/40 backdrop-blur-lg border border-neutral-700/50` のようなクラスを使用して、背景が上品に透けるグラスモーフィズムのコンテナを作成してください。」",
    demoComponent: "glass"
  },
  {
    name: "Gradient Text (グラデーション)",
    description: "文字色にソフトなグラデーションを適用し、上質な見出しを作るテクニック。視線を誘導する見出しに効果的。",
    prompt: "「テキストに `text-transparent bg-clip-text bg-linear-to-br from-neutral-200 to-neutral-500` を適用し、美しいグラデーションのタイポグラフィを作成してください。」",
    demoComponent: "gradientText"
  },
  {
    name: "Soft Glow (ソフトグロー)",
    description: "要素の周囲に控えめな影を落とし、柔らかく光を浴びているように見せる。ホバー時によく使われる。",
    prompt: "「ボタンのホバー時に、`shadow-md shadow-white/5` などのクラスを使用して、要素が柔らかい光を放っているような控えめなグローエフェクトを追加してください。」",
    demoComponent: "glow"
  },
  {
    name: "Skeleton (スケルトン)",
    description: "データ読み込み中に、要素の形だけを静かに表示。ユーザーの待機時間を心理的に軽減する。",
    prompt: "「`animate-pulse` クラス and `bg-neutral-800` を組み合わせた丸みのあるブロック配置し、読み込み中を示すミニマルなスケルトンUIを作成してください。」",
    demoComponent: "skeleton"
  }
]
</script>

<template>
  <div class="min-h-screen bg-neutral-900 text-stone-300 flex flex-col items-center selection:bg-stone-100/10 font-sans">
    
    <!-- Header Area -->
    <header class="w-full max-w-6xl px-8 py-20">
      <div class="inline-flex items-center gap-3 mb-6">
        <div class="w-10 h-[1px] bg-neutral-700 text-sm"></div>
        <span class="text-xs font-bold text-neutral-500 tracking-[0.2em] uppercase">VibeCoding UI</span>
      </div>
      <h1 class="text-5xl md:text-7xl font-extrabold tracking-tight text-white mb-8 leading-[1.1]">
        UI Dictionary<br />
        <span class="text-neutral-600">for AI Assistants</span>
      </h1>
      <p class="text-neutral-500 text-xl max-w-2xl leading-relaxed font-medium">
        温もりを感じるグレーと、鮮明なパールホワイト。<br>AIと共感・共創するための洗練されたリファレンス。
      </p>
    </header>

    <main class="w-full max-w-6xl px-8 pb-40 flex-1">
      <!-- Main Tabs Navigation -->
      <nav class="flex items-center gap-12 border-b border-neutral-800 mb-20 relative">
        <button
          @click="activeTab = 'general'"
          :class="['pb-6 text-sm font-bold tracking-wider transition-all duration-300 border-b-2 z-10', activeTab === 'general' ? 'border-white text-white' : 'border-transparent text-neutral-600 hover:text-neutral-400']"
        >
          General Components
        </button>
        <button
          @click="activeTab = 'tailwind'"
          :class="['pb-6 text-sm font-bold tracking-wider transition-all duration-300 border-b-2 z-10', activeTab === 'tailwind' ? 'border-white text-white' : 'border-transparent text-neutral-600 hover:text-neutral-400']"
        >
          Tailwind Patterns
        </button>
      </nav>

      <!-- Contents Area -->
      <div class="relative min-h-[600px]">
        <Transition name="page" mode="out-in">
          
          <!-- General Components Tab -->
          <div v-if="activeTab === 'general'" key="general" class="flex flex-col md:flex-row gap-16">
            
            <!-- Sidebar Navigation -->
            <aside class="w-full md:w-64 shrink-0 flex flex-col gap-1">
              <h3 class="text-[10px] font-black uppercase tracking-[0.3em] text-neutral-500 mb-6 pl-4 border-l border-neutral-800 py-1">Genres</h3>
              <button
                v-for="genre in generalGenres"
                :key="genre.id"
                @click="activeGenreId = genre.id"
                class="text-left px-4 py-3 rounded-xl text-sm font-bold transition-all relative"
                :class="activeGenreId === genre.id ? 'text-white bg-white/5' : 'text-neutral-600 hover:text-neutral-400 hover:bg-white/2'"
              >
                <!-- Selection indicator -->
                <div v-if="activeGenreId === genre.id" class="absolute left-0 top-1/2 -translate-y-1/2 w-1 h-4 bg-white rounded-r-full shadow-[0_0_10px_white]"></div>
                {{ genre.name }}
              </button>
            </aside>

            <!-- Main Listing Area -->
            <div class="flex-1" v-if="activeGenre">
              <div class="mb-16 pb-8 border-b border-neutral-800/50">
                <h2 class="text-3xl md:text-4xl font-black text-white mb-4 tracking-tight">{{ activeGenre.name }}</h2>
                <p class="text-neutral-500 text-lg leading-relaxed">{{ activeGenre.description }}</p>
              </div>

              <!-- Genre Parts List: Cards -->
              <div class="space-y-24">
                <div v-for="(item, index) in activeGenre.parts" :key="index" class="relative group">
                  
                  <!-- Part Card Structure: Vertical & Clean -->
                  <div class="flex flex-col gap-10">
                    <!-- 1. Name Section -->
                    <div class="flex items-baseline gap-4">
                      <span class="text-neutral-700 font-mono text-sm">0{{ index + 1 }}.</span>
                      <h3 class="text-3xl font-black text-stone-100 tracking-tight group-hover:text-white transition-colors">{{ item.name }}</h3>
                    </div>

                    <!-- 2. Demo Image (Preview) Section -->
                    <div class="w-full aspect-video bg-[#121212] border border-neutral-800 rounded-3xl flex flex-col items-center justify-center relative overflow-hidden shadow-inner group-hover:border-neutral-700 transition-all duration-500">
                      <!-- Grid paper background pattern for demo -->
                      <div class="absolute inset-0 opacity-[0.03] pointer-events-none bg-[radial-gradient(#e5e7eb_1px,transparent_1px)] [background-size:16px_16px]"></div>
                      
                      <template v-if="item.demoComponent === 'primary-button'">
                        <button class="px-10 py-4 bg-stone-100 text-neutral-900 font-black rounded-xl transition-all hover:bg-white active:scale-95 shadow-2xl shadow-white/5">
                          Button
                        </button>
                      </template>
                      
                      <template v-else-if="item.demoComponent === 'secondary-button'">
                        <button class="px-10 py-4 bg-transparent text-stone-300 font-bold rounded-xl border-2 border-neutral-700 transition-all hover:bg-neutral-800 active:scale-95">
                          Action
                        </button>
                      </template>

                      <template v-else-if="item.demoComponent === 'icon-button'">
                        <button class="w-16 h-16 flex items-center justify-center bg-neutral-800/50 rounded-2xl border border-neutral-700/50 text-stone-400 transition-all hover:text-white hover:border-neutral-500 active:scale-90">
                          <svg xmlns="http://www.w3.org/2000/svg" class="w-8 h-8" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5"><rect x="3" y="3" width="18" height="18" rx="2" ry="2"></rect><circle cx="8.5" cy="8.5" r="1.5"></circle><polyline points="21 15 16 10 5 21"></polyline></svg>
                        </button>
                      </template>
                      
                      <template v-else-if="item.demoComponent === 'dropdown'">
                        <div class="relative w-48 mt-12 scale-110">
                          <div class="absolute inset-x-0 bottom-4 bg-neutral-800 border-2 border-neutral-700 rounded-2xl shadow-2xl p-1 z-10 overflow-hidden">
                            <div class="px-4 py-2.5 text-xs font-bold text-stone-300 hover:bg-neutral-700/50 rounded-xl cursor-pointer transition-colors">Duplicate</div>
                            <div class="px-4 py-2.5 text-xs font-bold text-stone-300 hover:bg-neutral-700/50 rounded-xl cursor-pointer transition-colors">Copy Link</div>
                            <div class="px-4 py-2.5 text-xs font-bold text-red-400 hover:bg-red-400/5 rounded-xl cursor-pointer transition-colors">Archieve</div>
                          </div>
                        </div>
                      </template>

                      <template v-else-if="item.demoComponent === 'fab'">
                        <div class="absolute bottom-8 right-8 w-16 h-16 bg-white text-black rounded-full flex items-center justify-center shadow-2xl cursor-pointer transition-all hover:-translate-y-2 active:scale-90">
                          <svg xmlns="http://www.w3.org/2000/svg" class="w-7 h-7" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5"><line x1="12" y1="5" x2="12" y2="19"></line><line x1="5" y1="12" x2="19" y2="12"></line></svg>
                        </div>
                      </template>
                    </div>

                    <!-- 3. Description Section -->
                    <div class="max-w-2xl">
                      <div class="text-[9px] font-black uppercase tracking-widest text-neutral-600 mb-3 border-l-2 border-neutral-800 pl-3">Design Logic</div>
                      <p class="text-neutral-400 text-sm md:text-base leading-relaxed font-medium">{{ item.description }}</p>
                    </div>

                    <!-- 4. Prompt Section: Distinct Block -->
                    <div class="bg-neutral-800 border border-neutral-700/50 rounded-3xl p-8 relative group-hover:bg-[#202020] transition-colors">
                      <div class="flex items-center gap-2 mb-4 text-white">
                        <svg class="w-4 h-4" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2.5"><path stroke-linecap="round" stroke-linejoin="round" d="M13 10V3L4 14h7v7l9-11h-7z" /></svg>
                        <span class="text-xs font-black uppercase tracking-widest">✨ Prompt Guideline</span>
                      </div>
                      <p class="text-stone-100 text-sm md:text-base leading-relaxed italic font-serif">
                        {{ item.prompt }}
                      </p>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>

          <!-- Tailwind Patterns Tab -->
          <div v-else-if="activeTab === 'tailwind'" key="tailwind" class="grid grid-cols-1 md:grid-cols-2 gap-16">
            <div v-for="(item, index) in tailwindParts" :key="index" class="flex flex-col gap-6">
              <h3 class="text-2xl font-black text-stone-100">{{ item.name }}</h3>
              <div class="aspect-square bg-neutral-900 border border-neutral-800 rounded-3xl flex items-center justify-center relative overflow-hidden group">
                 <template v-if="item.demoComponent === 'glass'">
                    <div class="absolute inset-x-0 top-0 h-1/2 bg-neutral-700/30"></div>
                    <div class="w-2/3 h-1/2 bg-white/5 backdrop-blur-xl border border-white/10 p-6 rounded-2xl shadow-2xl relative">
                      <div class="h-4 w-1/3 bg-white/20 rounded"></div>
                    </div>
                  </template>
                  <template v-if="item.demoComponent === 'gradientText'">
                    <h2 class="text-4xl font-black text-transparent bg-clip-text bg-linear-to-br from-neutral-100 to-neutral-600">
                      Elegant
                    </h2>
                  </template>
              </div>
              <p class="text-neutral-500 text-sm leading-relaxed">{{ item.description }}</p>
              <div class="bg-white/5 border border-white/10 p-6 rounded-2xl italic text-stone-200 text-sm">
                {{ item.prompt }}
              </div>
            </div>
          </div>
        </Transition>
      </div>
    </main>

    <!-- Footer -->
    <footer class="w-full max-w-6xl px-8 py-20 border-t border-neutral-800/50 flex justify-between items-center text-[10px] font-black uppercase tracking-widest text-neutral-600">
      <span>VibeCoding UI Encyclopedia</span>
      <div class="flex gap-8">
        <a href="#" class="hover:text-stone-300 transition-colors">Documentation</a>
        <a href="#" class="hover:text-stone-300 transition-colors">About</a>
      </div>
    </footer>
  </div>
</template>

<style scoped>
.page-enter-active,
.page-leave-active {
  transition: opacity 0.4s cubic-bezier(0.23, 1, 0.32, 1), transform 0.4s cubic-bezier(0.23, 1, 0.32, 1);
}
.page-enter-from { opacity: 0; transform: translateY(10px); }
.page-leave-to { opacity: 0; transform: translateY(-10px); }
</style>
