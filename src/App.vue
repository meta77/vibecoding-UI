<script setup lang="ts">
import { ref } from 'vue'

const activeTab = ref<'general' | 'tailwind'>('general')

const generalParts = [
  {
    name: "Button (ボタン)",
    description: "ユーザーの操作をトリガーするための要素。主要なアクション（Primary）と副次的なアクション（Secondary）などで視覚的な重みを変えるのが一般的。",
    prompt: "「〇〇ボタンを作って」ではなく、「ホバー時に背景がわずかに明るくなり、アクティブ時にスケールダウンするアニメーションを持つ、角丸のPrimaryボタンを作成してください」と状態やインタラクションを具体的に指示する。",
    demoComponent: "button"
  },
  {
    name: "Card (カード)",
    description: "情報をグループ化して表示するコンテナ。画像、テキスト、アクション要素をまとめるのに適している。",
    prompt: "「カードUIを書いて」ではなく、「上部に画像プレースホルダー、中央にタイトルと説明文、下部に右寄せのアクションボタンを配置した、柔らかな影と角丸のカードを作成してください」と構造を伝える。",
    demoComponent: "card"
  },
  {
    name: "Modal / Dialog (モーダル)",
    description: "現在の画面を維持したまま、手前に重なって表示されるウィンドウ。重要な確認や入力を求める際に使用する。",
    prompt: "「背景を半透明の暗いグレーで覆うオーバーレイを敷き、画面中央に静かに現れる角丸のダイアログボックスを作成してください。トランジション（フェードイン）もつけてください。」",
    demoComponent: "modal"
  },
  {
    name: "Input / Form (入力フォーム)",
    description: "ユーザーからのテキスト入力を受け付ける。入力状態（Focus, Error, Disabled）の視覚的フィードバックが重要。",
    prompt: "「フォーカス時にボーダーが明るいパールホワイトになり、わずかに光がにじむような、ラベル付きの入力フォームを作成してください。エラー時のスタイルも含めてください。」",
    demoComponent: "input"
  }
]

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
    <header class="w-full max-w-5xl px-8 py-20">
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

    <main class="w-full max-w-5xl px-8 pb-32 flex-1">
      <!-- Tabs -->
      <nav class="flex items-center gap-12 border-b border-neutral-800 mb-20">
        <button
          @click="activeTab = 'general'"
          :class="[
            'pb-6 text-sm font-bold tracking-wider transition-all duration-300 border-b-2',
            activeTab === 'general' ? 'border-white text-white' : 'border-transparent text-neutral-600 hover:text-neutral-400'
          ]"
        >
          General Components
        </button>
        <button
          @click="activeTab = 'tailwind'"
          :class="[
            'pb-6 text-sm font-bold tracking-wider transition-all duration-300 border-b-2',
            activeTab === 'tailwind' ? 'border-white text-white' : 'border-transparent text-neutral-600 hover:text-neutral-400'
          ]"
        >
          Tailwind Patterns
        </button>
      </nav>

      <!-- Tab Contents -->
      <div class="relative min-h-[600px]">
        <Transition name="page" mode="out-in">
          <!-- General Tab -->
          <div v-if="activeTab === 'general'" key="general" class="grid grid-cols-1 md:grid-cols-2 gap-12">
            <div v-for="(item, index) in generalParts" :key="index" class="group">
              <!-- Demo Area -->
              <div class="aspect-video bg-neutral-900 border border-neutral-800 rounded-2xl mb-8 flex flex-col items-center justify-center relative overflow-hidden transition-all duration-500 group-hover:border-neutral-700 group-hover:bg-[#1E1E1E]">
                
                <template v-if="item.demoComponent === 'button'">
                  <button class="px-8 py-3 bg-white text-black font-bold rounded-full transition-all hover:scale-105 active:scale-95">
                    Action
                  </button>
                  <button class="mt-6 px-8 py-3 bg-neutral-800 text-stone-400 font-bold rounded-full border border-neutral-700 transition-all hover:bg-neutral-700">
                    Secondary
                  </button>
                </template>
                
                <template v-else-if="item.demoComponent === 'card'">
                  <div class="w-2/3 bg-neutral-800 border border-neutral-700 p-6 rounded-2xl shadow-xl">
                    <div class="w-12 h-12 bg-neutral-700 rounded-lg mb-4"></div>
                    <div class="h-4 w-3/4 bg-neutral-600 rounded mb-2"></div>
                    <div class="h-3 w-1/2 bg-neutral-700 rounded"></div>
                  </div>
                </template>
                
                <template v-else-if="item.demoComponent === 'modal'">
                  <div class="absolute inset-0 bg-black/40 backdrop-blur-sm flex items-center justify-center p-6">
                    <div class="w-full bg-neutral-800 border border-neutral-700 rounded-2xl p-6 shadow-2xl scale-100">
                      <div class="h-4 w-1/3 bg-neutral-600 rounded mb-4"></div>
                      <div class="h-3 w-full bg-neutral-700 rounded mb-6"></div>
                      <div class="flex justify-end gap-3">
                        <div class="h-10 w-20 bg-neutral-700 rounded-full"></div>
                        <div class="h-10 w-24 bg-white rounded-full"></div>
                      </div>
                    </div>
                  </div>
                </template>

                <template v-else-if="item.demoComponent === 'input'">
                  <div class="w-2/3 space-y-4">
                    <div>
                      <div class="text-[10px] uppercase tracking-widest text-neutral-500 font-bold mb-2">Label</div>
                      <input type="text" value="Input focus state" class="w-full bg-neutral-800 border-2 border-white rounded-xl px-4 py-3 text-sm text-white focus:outline-none" readonly>
                    </div>
                  </div>
                </template>
              </div>

              <!-- Text Content -->
              <h3 class="text-xl font-bold mb-3">{{ item.name }}</h3>
              <p class="text-neutral-500 text-sm leading-relaxed mb-8">{{ item.description }}</p>
              
              <div class="bg-neutral-800 p-6 rounded-2xl border-l-4 border-white transition-all group-hover:bg-neutral-800/80">
                <div class="text-[10px] font-black uppercase tracking-[0.2em] text-neutral-400 mb-3">Effective Prompting</div>
                <p class="text-stone-300 text-sm leading-relaxed italic font-medium">
                  {{ item.prompt }}
                </p>
              </div>
            </div>
          </div>

          <!-- Tailwind Tab -->
          <div v-else-if="activeTab === 'tailwind'" key="tailwind" class="grid grid-cols-1 md:grid-cols-2 gap-12">
            <div v-for="(item, index) in tailwindParts" :key="index" class="group">
              <!-- Demo Area -->
              <div class="aspect-video bg-neutral-900 border border-neutral-800 rounded-2xl mb-8 flex flex-col items-center justify-center relative overflow-hidden transition-all duration-500 group-hover:border-neutral-700 group-hover:bg-[#1E1E1E]">
                
                <template v-if="item.demoComponent === 'glass'">
                  <div class="absolute inset-x-0 top-0 h-1/2 bg-neutral-700/50"></div>
                  <div class="w-2/3 h-1/2 bg-neutral-100/5 backdrop-blur-xl border border-white/10 p-6 rounded-2xl shadow-2xl relative">
                    <div class="h-4 w-1/3 bg-white/20 rounded"></div>
                  </div>
                </template>
                
                <template v-else-if="item.demoComponent === 'gradientText'">
                  <h2 class="text-4xl md:text-5xl font-black text-transparent bg-clip-text bg-linear-to-br from-neutral-200 to-neutral-600">
                    Sophisticated
                  </h2>
                </template>

                <template v-else-if="item.demoComponent === 'glow'">
                  <button class="px-8 py-3 bg-neutral-800 border border-neutral-700 text-stone-100 font-bold rounded-xl shadow-[0_0_20px_rgba(255,255,255,0.05)] transition-all hover:bg-neutral-700">
                    Subtle Glow
                  </button>
                </template>

                <template v-else-if="item.demoComponent === 'skeleton'">
                  <div class="w-2/3 flex gap-4">
                    <div class="w-12 h-12 rounded-full bg-neutral-800 animate-pulse"></div>
                    <div class="flex-1 space-y-3">
                      <div class="h-4 bg-neutral-800 rounded-full animate-pulse w-3/4"></div>
                      <div class="h-3 bg-neutral-800 rounded-full animate-pulse w-1/2"></div>
                    </div>
                  </div>
                </template>
              </div>

              <!-- Text Content -->
              <h3 class="text-xl font-bold mb-3">{{ item.name }}</h3>
              <p class="text-neutral-500 text-sm leading-relaxed mb-8">{{ item.description }}</p>
              
              <div class="bg-neutral-800 p-6 rounded-2xl border-l-4 border-white transition-all group-hover:bg-neutral-800/80">
                <div class="text-[10px] font-black uppercase tracking-[0.2em] text-neutral-400 mb-3">Tailwind Instruction</div>
                <p class="text-stone-300 text-sm leading-relaxed italic font-medium">
                  {{ item.prompt }}
                </p>
              </div>
            </div>
          </div>
        </Transition>
      </div>
    </main>

    <footer class="w-full max-w-5xl px-8 py-16 border-t border-neutral-800 text-xs font-bold tracking-widest text-neutral-600 uppercase flex justify-between">
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
  transform: translateY(20px);
}
.page-leave-to {
  opacity: 0;
  transform: translateY(-20px);
}
</style>
