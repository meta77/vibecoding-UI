<script setup lang="ts">
import { ref } from 'vue'

const activeTab = ref<'general' | 'tailwind'>('general')

const generalParts = [
  {
    name: "Button (ボタン)",
    description: "ユーザーの操作をトリガーするための要素。主要なアクション（Primary）と副次的なアクション（Secondary）などで視覚的な重みを変えるのが一般的。",
    prompt: "「〇〇ボタンを作って」ではなく、「ホバー時に少し明るくなり、クリック時に押し込まれるアニメーションを持つ、角丸のPrimaryボタンを作成してください」と状態やインタラクションを具体的に指示する。",
    demoComponent: "button"
  },
  {
    name: "Card (カード)",
    description: "情報をグループ化して表示するコンテナ。画像、テキスト、アクション要素をまとめるのに適している。",
    prompt: "「カードUIを書いて」ではなく、「上部に画像プレースホルダー、中央にタイトルと説明文、下部に右寄せのアクションボタンを配置した、ドロップシャドウと丸みのあるカードを作成してください」と構造を伝える。",
    demoComponent: "card"
  },
  {
    name: "Modal / Dialog (モーダル)",
    description: "現在の画面を維持したまま、手前に重なって表示されるウィンドウ。重要な確認や入力を求める際に使用する。",
    prompt: "「背景を半透明の黒で覆うオーバーレイを敷き、画面中央に固定された角丸のダイアログボックスを作成してください。トランジション（フェードイン・スケールアップ）もつけてください。」",
    demoComponent: "modal"
  },
  {
    name: "Input / Form (入力フォーム)",
    description: "ユーザーからのテキスト入力を受け付ける。入力状態（Focus, Error, Disabled）の視覚的フィードバックが重要。",
    prompt: "「フォーカス時にボーダーがPrimaryカラーに変わり、わずかにシャドウ（ring）が追加される、ラベル付きの入力フォームを作成してください。エラー時の赤枠状態のスタイルも含めてください。」",
    demoComponent: "input"
  }
]

const tailwindParts = [
  {
    name: "Glassmorphism (グラスモーフィズム)",
    description: "背景がすりガラスのように透けて見える、モダンでプレミアムなUI表現。",
    prompt: "「Tailwindの `bg-white/10 backdrop-blur-md border border-white/20` のようなクラスを使用して、背景が美しく透けるグラスモーフィズムのコンテナを作成してください。」",
    demoComponent: "glass"
  },
  {
    name: "Gradient Text (グラデーションテキスト)",
    description: "文字色にインラインでグラデーションを適用し、目を引く見出しを作るテクニック。",
    prompt: "「テキストに `text-transparent bg-clip-text bg-gradient-to-r from-blue-400 to-emerald-400` を適用し、美しいグラデーションのタイポグラフィを作成してください。」",
    demoComponent: "gradientText"
  },
  {
    name: "Glow / Neon Effect (発光エフェクト)",
    description: "ボタンやカードの周囲に色付きの影を落とし、ネオンサインのように発光しているように見せる表現。",
    prompt: "「ボタンのホバー時に、`shadow-lg shadow-blue-500/50` などのクラスを使用して、ボタン自体が発光しているようなグローエフェクトを追加してください。」",
    demoComponent: "glow"
  },
  {
    name: "Skeleton Loading (スケルトン)",
    description: "データ読み込み中に、要素の形だけを灰色で表示し、ローディング中であることを示すUI。",
    prompt: "「`animate-pulse` クラスと `bg-slate-700` を組み合わせた丸みのあるブロック配置し、3行のテキスト読み込み中を示すスケルトンローディングUIを作成してください。」",
    demoComponent: "skeleton"
  }
]
</script>

<template>
  <div class="min-h-screen bg-slate-900 text-slate-100 flex flex-col items-center selection:bg-indigo-500/30 font-sans">
    <header class="w-full max-w-5xl px-6 py-16 text-center">
      <div class="inline-block mb-4 px-3 py-1 rounded-full bg-slate-800 border border-slate-700 text-xs font-semibold text-indigo-400 tracking-wider">
        AI ASSISTANT DICTIONARY
      </div>
      <h1 class="text-4xl md:text-6xl font-extrabold tracking-tight text-transparent bg-clip-text bg-gradient-to-r from-indigo-400 via-blue-400 to-teal-400 mb-6 drop-shadow-sm">
        VibeCoding UI Dictionary
      </h1>
      <p class="text-slate-400 text-lg md:text-xl max-w-2xl mx-auto leading-relaxed">
        AIへの効果的なプロンプトとともに、モダンなUIパーツの実装方法と名称を学ぶためのリファレンスサイト
      </p>
    </header>

    <main class="w-full max-w-5xl px-6 pb-24 flex-1">
      <!-- Tabs -->
      <div class="flex flex-wrap items-center justify-center gap-2 p-1.5 bg-slate-800/60 backdrop-blur-sm rounded-2xl border border-slate-700/50 mb-12 w-fit mx-auto relative z-10 shadow-xl shadow-black/20">
        <button
          @click="activeTab = 'general'"
          :class="[
            'px-6 py-3 rounded-xl text-sm font-semibold transition-all duration-300 ease-out',
            activeTab === 'general' ? 'bg-indigo-500/10 text-indigo-300 border border-indigo-500/20 shadow-[0_0_15px_rgba(99,102,241,0.15)]' : 'text-slate-400 border border-transparent hover:text-slate-200 hover:bg-slate-700/50'
          ]"
        >
          <span class="flex items-center gap-2">
            <svg class="w-4 h-4" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2"><rect x="3" y="3" width="18" height="18" rx="2" ry="2"></rect></svg>
            一般的な Web UIパーツ
          </span>
        </button>
        <button
          @click="activeTab = 'tailwind'"
          :class="[
            'px-6 py-3 rounded-xl text-sm font-semibold transition-all duration-300 ease-out',
            activeTab === 'tailwind' ? 'bg-teal-500/10 text-teal-300 border border-teal-500/20 shadow-[0_0_15px_rgba(20,184,166,0.15)]' : 'text-slate-400 border border-transparent hover:text-slate-200 hover:bg-slate-700/50'
          ]"
        >
          <span class="flex items-center gap-2">
            <svg class="w-4 h-4" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2"><path stroke-linecap="round" stroke-linejoin="round" d="M13 10V3L4 14h7v7l9-11h-7z" /></svg>
            Tailwind CSS UIパーツ
          </span>
        </button>
      </div>

      <!-- Tab Contents -->
      <div class="relative">
        <Transition name="fade" mode="out-in">
          <!-- General Tab -->
          <div v-if="activeTab === 'general'" key="general" class="space-y-12">
            <div class="flex flex-col items-center text-center max-w-3xl mx-auto mb-16">
              <h2 class="text-2xl md:text-3xl font-bold text-white mb-4">
                構造と役割を伝える
              </h2>
              <p class="text-slate-400">
                システム全体で共通して使用される基礎的なUIコンポーネントです。AIへの指示では「どのような役割か」「どのような状態（Hover, Active, Error等）を持つか」を明確に伝えることが重要です。
              </p>
            </div>
            
            <div class="grid grid-cols-1 md:grid-cols-2 gap-8">
              <div v-for="(item, index) in generalParts" :key="index" class="group bg-slate-800/40 border border-slate-700/50 rounded-3xl p-6 hover:bg-slate-800/60 hover:border-indigo-500/30 transition-all duration-300 overflow-hidden relative">
                <!-- Background glow effect on hover -->
                <div class="absolute -inset-px bg-gradient-to-r from-indigo-500/0 via-indigo-500/0 to-indigo-500/0 group-hover:via-indigo-500/10 rounded-3xl blur-md transition-all duration-500 -z-10"></div>
                
                <!-- Demo Component Area -->
                <div class="h-48 bg-slate-900/80 rounded-2xl mb-6 flex flex-col items-center justify-center border border-slate-800 overflow-hidden relative p-4">
                  <!-- Button Demo -->
                  <template v-if="item.demoComponent === 'button'">
                    <button class="px-6 py-3 bg-indigo-600 hover:bg-indigo-500 active:scale-95 active:bg-indigo-700 rounded-xl text-white font-medium transition-all shadow-lg shadow-indigo-500/25">
                      Primary Button
                    </button>
                    <button class="mt-4 px-6 py-3 bg-slate-800 hover:bg-slate-700 active:scale-95 rounded-xl text-slate-300 font-medium transition-all border border-slate-700">
                      Secondary Action
                    </button>
                  </template>
                  
                  <!-- Card Demo -->
                  <template v-else-if="item.demoComponent === 'card'">
                    <div class="w-full max-w-sm bg-slate-800 border border-slate-700 rounded-xl overflow-hidden shadow-xl">
                      <div class="h-16 bg-gradient-to-r from-slate-700 to-slate-600"></div>
                      <div class="p-4">
                        <div class="h-4 w-1/3 bg-slate-600 rounded mb-2"></div>
                        <div class="h-3 w-3/4 bg-slate-700 rounded mb-4"></div>
                        <div class="flex justify-end"><div class="h-8 w-16 bg-indigo-600 rounded"></div></div>
                      </div>
                    </div>
                  </template>
                  
                  <!-- Modal Demo -->
                  <template v-else-if="item.demoComponent === 'modal'">
                    <div class="absolute inset-0 bg-slate-950/60 backdrop-blur-[2px] flex items-center justify-center z-10">
                      <div class="w-3/4 bg-slate-800 border border-slate-700 rounded-xl shadow-2xl p-4 transform scale-100 transition-transform">
                        <div class="flex justify-between items-center mb-3">
                          <div class="h-4 w-1/3 bg-slate-600 rounded"></div>
                          <div class="h-6 w-6 rounded-full bg-slate-700 flex items-center justify-center text-xs text-slate-400">×</div>
                        </div>
                        <div class="h-3 w-full bg-slate-700 rounded mb-2"></div>
                        <div class="h-3 w-5/6 bg-slate-700 rounded mb-4"></div>
                        <div class="flex justify-end gap-2 text-xs">
                          <div class="h-7 w-16 bg-slate-700 rounded"></div>
                          <div class="h-7 w-20 bg-indigo-600 rounded"></div>
                        </div>
                      </div>
                    </div>
                  </template>

                  <!-- Input Demo -->
                  <template v-else-if="item.demoComponent === 'input'">
                    <div class="w-full max-w-xs space-y-4">
                      <div>
                        <label class="block text-xs text-slate-400 mb-1">Email (Focus)</label>
                        <input type="text" value="user@example.com" class="w-full bg-slate-900 border border-indigo-500 rounded-lg px-3 py-2 text-sm text-slate-200 focus:outline-none ring-2 ring-indigo-500/20" readonly>
                      </div>
                      <div>
                        <label class="block text-xs text-slate-400 mb-1">Password (Error)</label>
                        <input type="password" value="123" class="w-full bg-slate-900 border border-red-500 rounded-lg px-3 py-2 text-sm text-slate-200 focus:outline-none" readonly>
                        <span class="text-[10px] text-red-400 mt-1 block">パスワードが短すぎます</span>
                      </div>
                    </div>
                  </template>
                </div>

                <h3 class="text-xl font-bold text-slate-100 mb-3">{{ item.name }}</h3>
                <p class="text-slate-400 text-sm mb-6 leading-relaxed">{{ item.description }}</p>
                
                <div class="bg-indigo-950/30 rounded-2xl p-5 border border-indigo-500/20 group-hover:border-indigo-500/40 transition-colors">
                  <div class="flex items-center text-xs text-indigo-400 font-bold mb-3 tracking-widest uppercase">
                    <svg class="w-4 h-4 mr-2" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 10V3L4 14h7v7l9-11h-7z" /></svg>
                    AI プロンプト例
                  </div>
                  <p class="text-slate-300 text-sm leading-relaxed font-medium">
                    {{ item.prompt }}
                  </p>
                </div>
              </div>
            </div>
          </div>

          <!-- Tailwind Tab -->
          <div v-else-if="activeTab === 'tailwind'" key="tailwind" class="space-y-12">
            <div class="flex flex-col items-center text-center max-w-3xl mx-auto mb-16">
              <h2 class="text-2xl md:text-3xl font-bold text-white mb-4">
                クラスと表現を伝える
              </h2>
              <p class="text-slate-400">
                ユーティリティファーストなCSSフレームワークであるTailwind CSSならではの表現です。AIに具体的なクラス群を例示することで、一発で高品質なデザインを生成させることができます。
              </p>
            </div>
            
            <div class="grid grid-cols-1 md:grid-cols-2 gap-8">
              <div v-for="(item, index) in tailwindParts" :key="index" class="group bg-slate-800/40 border border-slate-700/50 rounded-3xl p-6 hover:bg-slate-800/60 hover:border-teal-500/30 transition-all duration-300 overflow-hidden relative">
                <!-- Background glow effect on hover -->
                <div class="absolute -inset-px bg-gradient-to-r from-teal-500/0 via-teal-500/0 to-teal-500/0 group-hover:via-teal-500/10 rounded-3xl blur-md transition-all duration-500 -z-10"></div>
                
                <!-- Demo Component Area -->
                <div class="h-48 bg-slate-900/80 rounded-2xl mb-6 flex flex-col items-center justify-center border border-slate-800 overflow-hidden relative p-4"
                     :class="{'bg-[url(https://images.unsplash.com/photo-1618005182384-a83a8bd57fbe?q=80&w=600&auto=format&fit=crop)] bg-cover bg-center': item.demoComponent === 'glass'}">
                  
                  <!-- Glass Demo -->
                  <template v-if="item.demoComponent === 'glass'">
                    <div class="absolute inset-0 bg-slate-900/40 mix-blend-multiply"></div>
                    <div class="relative w-4/5 h-3/4 bg-white/10 backdrop-blur-md border border-white/20 rounded-2xl p-5 shadow-2xl flex flex-col justify-center">
                      <div class="h-4 w-1/2 bg-white/40 rounded mb-3"></div>
                      <div class="h-2 w-full bg-white/20 rounded mb-2"></div>
                      <div class="h-2 w-3/4 bg-white/20 rounded"></div>
                    </div>
                  </template>
                  
                  <!-- Gradient Text Demo -->
                  <template v-else-if="item.demoComponent === 'gradientText'">
                    <h2 class="text-4xl md:text-5xl font-black text-transparent bg-clip-text bg-gradient-to-br from-indigo-400 via-purple-400 to-pink-400">
                      Beautiful Text
                    </h2>
                  </template>

                  <!-- Glow Demo -->
                  <template v-else-if="item.demoComponent === 'glow'">
                    <button class="px-8 py-4 bg-slate-800 rounded-2xl border border-teal-500/50 text-teal-400 font-bold shadow-[0_0_20px_rgba(20,184,166,0.4)] transition-all animate-pulse">
                      Glowing Button
                    </button>
                  </template>

                  <!-- Skeleton Demo -->
                  <template v-else-if="item.demoComponent === 'skeleton'">
                    <div class="w-full max-w-sm flex space-x-4">
                      <div class="w-12 h-12 rounded-full bg-slate-700 animate-pulse"></div>
                      <div class="flex-1 space-y-3 py-1">
                        <div class="h-3 bg-slate-700 rounded animate-pulse w-3/4"></div>
                        <div class="space-y-2">
                          <div class="h-3 bg-slate-700 rounded animate-pulse"></div>
                          <div class="h-3 bg-slate-700 rounded animate-pulse w-5/6"></div>
                        </div>
                      </div>
                    </div>
                  </template>
                </div>

                <h3 class="text-xl font-bold text-slate-100 mb-3">{{ item.name }}</h3>
                <p class="text-slate-400 text-sm mb-6 leading-relaxed">{{ item.description }}</p>
                
                <div class="bg-teal-950/30 rounded-2xl p-5 border border-teal-500/20 group-hover:border-teal-500/40 transition-colors">
                  <div class="flex items-center text-xs text-teal-400 font-bold mb-3 tracking-widest uppercase">
                    <svg class="w-4 h-4 mr-2" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 10V3L4 14h7v7l9-11h-7z" /></svg>
                    AI プロンプト例
                  </div>
                  <p class="text-slate-300 text-sm leading-relaxed font-medium">
                    {{ item.prompt }}
                  </p>
                </div>
              </div>
            </div>
          </div>
        </Transition>
      </div>
    </main>

    <footer class="w-full max-w-5xl px-6 py-8 border-t border-slate-800/50 text-center text-sm text-slate-500">
      <p>&copy; 2026 VibeCoding UI Dictionary. Built with Vite, Vue 3 & Tailwind CSS v4.</p>
    </footer>
  </div>
</template>

<style scoped>
/* Vue Transitions for nice tab switching */
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.4s ease, transform 0.4s ease;
}
.fade-enter-from {
  opacity: 0;
  transform: translateY(10px);
}
.fade-leave-to {
  opacity: 0;
  transform: translateY(-10px);
}
</style>
