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
        name: "Primary Button (主要)",
        description: "画面内で最も重要な操作を促すボタン。「次へ」「保存」などのアクションに使用。",
        prompt: "「ホバー時に背景がわずかに明るいグレーになり、アクティブ時にスケールダウンするアニメーションを持つ、角丸の完全にべた塗り（Solid）のPrimaryボタンを作成してください。色はパールホワイト（stone-100）で、文字は黒（neutral-900）にしてください。」",
        demoComponent: "primary-button"
      },
      {
        name: "Secondary Button",
        description: "キャンセルのような副次的な操作。アウトラインやゴーストスタイルが選ばれることが多い。",
        prompt: "「背景は透明で、細いボーダー（neutral-700）を持つOutlineボタンを作成してください。ホバー時に入力エリアと同じように背景色がわずかに明るいグレー（neutral-800）になるように指定してください。」",
        demoComponent: "secondary-button"
      },
      {
        name: "Icon Button",
        description: "テキストを用いず、アイコンのみで機能を示す。ツールバー内の省スペースなアクションに最適。",
        prompt: "「正方形から角丸（rounded-lg）にし、中央にSVGアイコンを配置したアイコンボタンを作成してください。ホバー時に丸い灰色の背景（bg-neutral-800）がフェードインするような心地よいインタラクションを与えてください。」",
        demoComponent: "icon-button"
      },
      {
        name: "Dropdown Menu",
        description: "クリック時に展開されるアクションリスト。設定や多機能なアクションをスッキリとまとめる。",
        prompt: "「ボタン押下で下部にフロートするドロップダウンメニューを作成してください。メニュー本体は背景暗めのグレー（neutral-800/90）、うっすらとしたボーダー（neutral-700）、ドロップシャドウを付け、各アイテムはホバーで色が変わるように設計してください。」",
        demoComponent: "dropdown"
      },
      {
        name: "Floating Action Button",
        description: "画面右下などに常に固定表示されるボタン。モバイルでの「新規作成」などに使われる。",
        prompt: "「画面の右下に絶対配置（fixed）された円形のシャドウ付きボタンを作成してください。色は白（bg-white）で、スクロールしても常に手前（z-50）に被さるようにし、ホバー時にはフワッと少し浮き上がる（-translate-y-1）ようにしてください。」",
        demoComponent: "fab"
      }
    ]
  },
  {
    id: 'input',
    name: 'Input & Forms',
    description: 'ユーザーからの情報を収集し、正確に入力してもらうためのパーツ。',
    parts: [
      {
        name: "Text Input (基本入力)",
        description: "最も基本的な入力要素。プレースホルダー、フォーカス時の視覚的フィードバック（グロー効果など）が重要。",
        prompt: "「背景が `neutral-800`、境界線が `neutral-700`、フォーカス時に `stone-100` の繊細なアウトラインを放つ、洗練された入力フィールドを作成してください。文字色は `stone-200` に設定してください。」",
        demoComponent: "text-input"
      },
      {
        name: "Checkbox (複数選択)",
        description: "ユーザーが複数のオプションを選択するためのパーツ。標準のブラウザスタイルを隠し、カスタムデザインにするのがモダン。",
        prompt: "「角丸の `neutral-800` の正方形ボックスで、チェックが入ると背景が `stone-100` になり、中に `neutral-900` のチェックアイコンが表示されるカスタムチェックボックスを作成してください。」",
        demoComponent: "checkbox"
      },
      {
        name: "Radio Button (単一選択)",
        description: "排他的な選択肢から一つを選ぶ。ドットの中心が光るような、触感を感じさせるデザインが好まれる。",
        prompt: "「円形の `neutral-800` の外枠の中に、選択時に `stone-100` の小さな円が浮かび上がるラジオボタンを作成してください。選択状態に応じてラベルの色も変わるように設計してください。」",
        demoComponent: "radio"
      },
      {
        name: "Toggle Switch (トグル)",
        description: "ON/OFFの即時切り替えを示す。滑らかなスライドアニメーションが、ユーザー体験を豊かにする。",
        prompt: "「幅広の角丸カプセル型の背景の中で、白い円形のつまみが左右に滑らかにスライドするトグルスイッチを作成してください。ONの時は背景が `neutral-700` に変化するようにしてください。」",
        demoComponent: "toggle"
      },
      {
        name: "Select Menu (セレクト)",
        description: "多くの選択肢がある場合に、場所を取らずに一つを選ばせる。ドロップダウン矢印の配置と、一貫したスタイルが鍵。",
        prompt: "「標準の `select` 要素をカスタムスタイルで隠し、右側に小さな下向き矢印アイコンを配置したセレクトメニューを作成してください。背景は `neutral-800`、フォーカス時に `border-stone-100` になるようにしてください。」",
        demoComponent: "select"
      }
    ]
  },
  { id: 'navigation', name: 'Navigation', description: '目的地に辿り着くためのパーツ。(準備中)', parts: [] },
  { id: 'container', name: 'Container & Layout', description: '情報をグループ化する器のパーツ。(準備中)', parts: [] },
  { id: 'feedback', name: 'Status & Feedback', description: 'システムの状態を画面上に返すパーツ。(準備中)', parts: [] }
]

const activeGenre = computed(() => generalGenres.find(g => g.id === activeGenreId.value))

const tailwindParts = [
  {
    name: "Glass (グラス)",
    description: "背景がすりガラスのように透けて見える、モダンで上質なUI表現。北欧風の清潔感あるデザインに最適。",
    prompt: "「Tailwindの \`bg-neutral-800/40 backdrop-blur-lg border border-neutral-700/50\` のようなクラスを使用して、背景が上品に透けるグラスモーフィズムのコンテナを作成してください。」",
    demoComponent: "glass"
  },
  {
    name: "Gradient Text (グラデーション)",
    description: "文字色にソフトなグラデーションを適用し、上質な見出しを作るテクニック。視線を誘導する見出しに効果的。",
    prompt: "「テキストに \`text-transparent bg-clip-text bg-linear-to-br from-neutral-200 to-neutral-500\` を適用し、美しいグラデーションのタイポグラフィを作成してください。」",
    demoComponent: "gradientText"
  },
  {
    name: "Soft Glow (ソフトグロー)",
    description: "要素の周囲に控えめな影を落とし、柔らかく光を浴びているように見せる。ホバー時によく使われる。",
    prompt: "「ボタンのホバー時に、\`shadow-md shadow-white/5\` などのクラスを使用して、要素が柔らかい光を放っているような控えめなグローエフェクトを追加してください。」",
    demoComponent: "glow"
  },
  {
    name: "Skeleton (スケルトン)",
    description: "データ読み込み中に、要素の形だけを静かに表示。ユーザーの待機時間を心理的に軽減する。",
    prompt: "「\`animate-pulse\` クラス and \`bg-neutral-800\` を組み合わせた丸みのあるブロック配置し、読み込み中を示すミニマルなスケルトンUIを作成してください。」",
    demoComponent: "skeleton"
  }
]
</script>

<template>
  <div class="min-h-screen bg-neutral-900 text-stone-300 flex flex-col items-center selection:bg-stone-100/10 font-sans">
    
    <!-- Header Area -->
    <header class="w-full max-w-7xl px-8 py-20">
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

    <main class="w-full max-w-7xl px-8 pb-40 flex-1">
      <!-- Main Tabs Navigation -->
      <nav class="flex items-center gap-12 border-b border-neutral-800 mb-16 relative">
        <button
          @click="activeTab = 'general'"
          :class="['pb-5 text-sm font-bold tracking-wider transition-all duration-300 border-b-2 z-10', activeTab === 'general' ? 'border-white text-white' : 'border-transparent text-neutral-600 hover:text-neutral-400']"
        >
          General Components
        </button>
        <button
          @click="activeTab = 'tailwind'"
          :class="['pb-5 text-sm font-bold tracking-wider transition-all duration-300 border-b-2 z-10', activeTab === 'tailwind' ? 'border-white text-white' : 'border-transparent text-neutral-600 hover:text-neutral-400']"
        >
          Tailwind Patterns
        </button>
      </nav>

      <!-- Contents Area -->
      <div class="relative min-h-[600px]">
        <Transition name="page" mode="out-in">
          
          <!-- General Components Tab -->
          <div v-if="activeTab === 'general'" key="general" class="flex flex-col lg:flex-row gap-12">
            
            <!-- Sidebar Navigation -->
            <aside class="w-full lg:w-56 shrink-0 flex flex-col gap-1">
              <h3 class="text-[10px] font-black uppercase tracking-[0.3em] text-neutral-500 mb-6 pl-4 border-l border-neutral-800 py-1">Genres</h3>
              <button
                v-for="genre in generalGenres"
                :key="genre.id"
                @click="activeGenreId = genre.id"
                class="text-left px-4 py-3 rounded-xl text-sm font-bold transition-all relative"
                :class="activeGenreId === genre.id ? 'text-white bg-white/5' : 'text-neutral-500 hover:text-neutral-300 hover:bg-white/2'"
              >
                <!-- Selection indicator -->
                <div v-if="activeGenreId === genre.id" class="absolute left-0 top-1/2 -translate-y-1/2 w-[3px] h-4 bg-white rounded-r-full shadow-[0_0_10px_white]"></div>
                {{ genre.name }}
              </button>
            </aside>

            <!-- Main Listing Area -->
            <div class="flex-1 min-w-0" v-if="activeGenre">
              <div class="mb-12 pb-6 border-b border-neutral-800/50">
                <h2 class="text-3xl font-black text-white mb-3 tracking-tight">{{ activeGenre.name }}</h2>
                <p class="text-neutral-500 text-base leading-relaxed">{{ activeGenre.description }}</p>
              </div>

              <!-- Genre Parts List: 2-Column Grid -->
              <div class="grid grid-cols-1 md:grid-cols-2 gap-8">
                <div v-for="(item, index) in activeGenre.parts" :key="index" class="relative group">
                  
                  <!-- Part Card Wrapping Container -->
                  <div class="flex flex-col h-full bg-[#1A1A1A] border border-neutral-800/80 rounded-[2rem] p-6 hover:border-neutral-700 transition-colors shadow-lg">
                    
                    <!-- 1. Name Section -->
                    <div class="flex items-center gap-3 mb-6">
                      <span class="text-neutral-600 font-mono text-xs opacity-50">0{{ index + 1 }}</span>
                      <h3 class="text-xl font-bold text-stone-100 tracking-tight group-hover:text-white transition-colors truncate">{{ item.name }}</h3>
                    </div>

                    <!-- 2. Demo Image (Preview) Section -->
                    <div class="w-full aspect-[4/3] bg-[#121212] border border-neutral-800/50 rounded-2xl flex flex-col items-center justify-center relative overflow-hidden shadow-inner mb-8 group-hover:bg-[#151515] transition-colors">
                      <!-- Grid paper background pattern for demo -->
                      <div class="absolute inset-0 opacity-[0.03] pointer-events-none bg-[radial-gradient(#e5e7eb_1px,transparent_1px)] [background-size:16px_16px]"></div>
                      
                      <!-- Action & Trigger Demos -->
                      <template v-if="item.demoComponent === 'primary-button'">
                        <button class="px-8 py-3 bg-stone-100 text-neutral-900 font-bold rounded-full transition-all hover:bg-white active:scale-95 shadow-xl shadow-white/5 text-sm">
                          Button
                        </button>
                      </template>
                      
                      <template v-else-if="item.demoComponent === 'secondary-button'">
                        <button class="px-8 py-3 bg-transparent text-stone-300 font-bold rounded-full border border-neutral-700 transition-all hover:bg-neutral-800 active:scale-95 text-sm">
                          Action
                        </button>
                      </template>

                      <template v-else-if="item.demoComponent === 'icon-button'">
                        <button class="w-12 h-12 flex items-center justify-center bg-neutral-800/50 rounded-xl border border-neutral-700/50 text-stone-400 transition-all hover:text-white hover:border-neutral-500 active:scale-90">
                          <svg xmlns="http://www.w3.org/2000/svg" class="w-6 h-6" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5"><rect x="3" y="3" width="18" height="18" rx="2" ry="2"></rect><circle cx="8.5" cy="8.5" r="1.5"></circle><polyline points="21 15 16 10 5 21"></polyline></svg>
                        </button>
                      </template>
                      
                      <template v-else-if="item.demoComponent === 'dropdown'">
                        <div class="relative w-40 scale-100">
                          <div class="bg-neutral-800 border-2 border-neutral-700 rounded-xl shadow-2xl p-1 overflow-hidden">
                            <div class="px-3 py-2 text-xs font-bold text-stone-300 hover:bg-neutral-700/50 rounded-lg cursor-pointer transition-colors">Duplicate</div>
                            <div class="px-3 py-2 text-xs font-bold text-stone-300 hover:bg-neutral-700/50 rounded-lg cursor-pointer transition-colors">Copy Link</div>
                            <div class="px-3 py-2 text-xs font-bold text-red-400 hover:bg-red-400/5 rounded-lg cursor-pointer transition-colors">Archieve</div>
                          </div>
                        </div>
                      </template>

                      <template v-else-if="item.demoComponent === 'fab'">
                        <div class="absolute bottom-6 right-6 w-12 h-12 bg-white text-black rounded-full flex items-center justify-center shadow-xl cursor-pointer transition-all hover:-translate-y-1 hover:shadow-white/20 active:scale-90">
                          <svg xmlns="http://www.w3.org/2000/svg" class="w-5 h-5" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5"><line x1="12" y1="5" x2="12" y2="19"></line><line x1="5" y1="12" x2="19" y2="12"></line></svg>
                        </div>
                      </template>

                      <!-- Input & Forms Demos -->
                      <template v-else-if="item.demoComponent === 'text-input'">
                        <div class="w-2/3">
                          <input type="text" placeholder="Sample Input" class="w-full bg-neutral-800 border border-neutral-700 rounded-xl px-4 py-2.5 text-sm text-stone-200 outline-none focus:border-stone-100 transition-all placeholder:text-neutral-600">
                        </div>
                      </template>

                      <template v-else-if="item.demoComponent === 'checkbox'">
                        <div class="flex items-center gap-4">
                          <div class="w-7 h-7 bg-stone-100 rounded-lg flex items-center justify-center text-neutral-900 shadow-lg shadow-white/5 cursor-pointer">
                            <svg xmlns="http://www.w3.org/2000/svg" class="w-5 h-5" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="3" stroke-linecap="round" stroke-linejoin="round"><polyline points="20 6 9 17 4 12"></polyline></svg>
                          </div>
                          <span class="text-sm font-bold text-stone-300">Checked</span>
                        </div>
                      </template>

                      <template v-else-if="item.demoComponent === 'radio'">
                        <div class="flex items-center gap-4">
                          <div class="w-7 h-7 rounded-full border-2 border-stone-100 flex items-center justify-center cursor-pointer">
                            <div class="w-3.5 h-3.5 rounded-full bg-stone-100"></div>
                          </div>
                          <span class="text-sm font-bold text-stone-100">Selected</span>
                        </div>
                      </template>

                      <template v-else-if="item.demoComponent === 'toggle'">
                        <div class="w-14 h-8 bg-neutral-700 rounded-full relative p-1 cursor-pointer transition-all">
                          <div class="absolute right-1 w-6 h-6 bg-white rounded-full shadow-lg"></div>
                        </div>
                      </template>

                      <template v-else-if="item.demoComponent === 'select'">
                        <div class="w-2/3 relative">
                          <div class="w-full bg-neutral-800 border border-neutral-700 rounded-xl px-4 py-2.5 text-sm text-stone-200 flex justify-between items-center cursor-pointer">
                            <span>Dropdown Option</span>
                            <svg xmlns="http://www.w3.org/2000/svg" class="w-4 h-4 text-neutral-500" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="m6 9 6 6 6-6"/></svg>
                          </div>
                        </div>
                      </template>
                    </div>

                    <!-- 3. Description Section -->
                    <div class="mb-6 flex-1">
                      <div class="text-[8px] font-black uppercase tracking-widest text-neutral-600 mb-2 border-l-2 border-neutral-700 pl-2">Design Logic</div>
                      <p class="text-neutral-400 text-sm leading-relaxed font-medium">{{ item.description }}</p>
                    </div>

                    <!-- 4. Prompt Section -->
                    <div class="bg-neutral-900 border border-neutral-800 rounded-2xl p-5 relative transition-colors group-hover:border-neutral-700/80">
                      <div class="flex items-center gap-2 mb-3 text-stone-300">
                        <svg class="w-3.5 h-3.5" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2.5"><path stroke-linecap="round" stroke-linejoin="round" d="M13 10V3L4 14h7v7l9-11h-7z" /></svg>
                        <span class="text-[10px] font-black uppercase tracking-widest">Prompt Guideline</span>
                      </div>
                      <p class="text-stone-300/80 text-xs leading-relaxed italic font-serif">
                        {{ item.prompt }}
                      </p>
                    </div>

                  </div>
                </div>
              </div>
            </div>
          </div>

          <!-- Tailwind Patterns Tab -->
          <div v-else-if="activeTab === 'tailwind'" key="tailwind" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
            <div v-for="(item, index) in tailwindParts" :key="index" class="flex flex-col bg-[#1A1A1A] border border-neutral-800/80 rounded-[2rem] p-6 h-full hover:border-neutral-700 transition-colors shadow-lg group">
              <h3 class="text-xl font-bold text-stone-100 mb-6 truncate">{{ item.name }}</h3>
              <div class="w-full aspect-square bg-[#121212] border border-neutral-800/50 rounded-2xl flex items-center justify-center relative overflow-hidden mb-6 group-hover:bg-[#151515] transition-colors">
                 <template v-if="item.demoComponent === 'glass'">
                    <div class="absolute inset-x-0 top-0 h-1/2 bg-neutral-700/30"></div>
                    <div class="w-2/3 h-1/2 bg-white/5 backdrop-blur-xl border border-white/10 p-4 rounded-xl shadow-2xl relative flex items-center justify-center">
                      <div class="h-2 w-1/2 bg-white/20 rounded"></div>
                    </div>
                  </template>
                  <template v-else-if="item.demoComponent === 'gradientText'">
                    <h2 class="text-3xl font-black text-transparent bg-clip-text bg-linear-to-br from-neutral-100 to-neutral-600">
                      Elegant
                    </h2>
                  </template>
                  <template v-else-if="item.demoComponent === 'glow'">
                    <div class="px-5 py-2.5 text-sm bg-neutral-800 border border-neutral-700 text-stone-100 font-bold rounded-lg shadow-[0_0_15px_rgba(255,255,255,0.05)]">
                      Subtle Glow
                    </div>
                  </template>
                  <template v-else-if="item.demoComponent === 'skeleton'">
                    <div class="w-3/4 flex gap-3">
                      <div class="w-8 h-8 rounded-full bg-neutral-800 animate-pulse shrink-0"></div>
                      <div class="flex-1 space-y-2 py-1">
                        <div class="h-2 bg-neutral-800 rounded-full animate-pulse w-3/4"></div>
                        <div class="h-2 bg-neutral-800 rounded-full animate-pulse w-1/2"></div>
                      </div>
                    </div>
                  </template>
              </div>
              <div class="mb-6 flex-1">
                <p class="text-neutral-400 text-sm leading-relaxed">{{ item.description }}</p>
              </div>
              <div class="bg-neutral-900 border border-neutral-800 rounded-2xl p-5 relative transition-colors group-hover:border-neutral-700/80">
                  <div class="flex items-center gap-2 mb-3 text-stone-300">
                    <svg class="w-3.5 h-3.5" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2.5"><path stroke-linecap="round" stroke-linejoin="round" d="M13 10V3L4 14h7v7l9-11h-7z" /></svg>
                    <span class="text-[10px] font-black uppercase tracking-widest">Tailwind Code</span>
                  </div>
                <p class="italic text-stone-300/80 text-xs font-serif leading-relaxed">
                  {{ item.prompt }}
                </p>
              </div>
            </div>
          </div>
        </Transition>
      </div>
    </main>

    <!-- Footer -->
    <footer class="w-full max-w-7xl px-8 py-16 border-t border-neutral-800/50 flex flex-col md:flex-row gap-6 justify-between items-center text-[10px] font-black uppercase tracking-widest text-neutral-600">
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
