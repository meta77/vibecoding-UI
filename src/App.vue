<script setup lang="ts">
import { ref, computed } from 'vue'

const activeTab = ref<'general' | 'tailwind' | 'tutorial'>('general')
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

const tutorialChapters = [
  {
    chapterTitle: "第1章：Tailwindの始め方",
    chapterDescription: "Vite環境へのTailwind v4の導入手法を解説します。",
    steps: [
      {
        id: "step1",
        title: "1. Vite + Tailwind v4 のインストール",
        description: "最新のフロントエンドツール「Vite（ヴィート）」を使い、素早くプロジェクトの土台を作成します。",
        code: "npm create vite@latest my-project\\ncd my-project\\nnpm install tailwindcss @tailwindcss/vite",
        insightLevel: "セットアップの極意",
        insightText: "Tailwind v4 から導入構成が劇的にシンプルになりました。PostCSSなどの複雑な設定ファイルは不要で、Viteプラグインを一つ入れるだけで最速のモダン開発環境が整います。",
        demoTitle: "ターミナル実行イメージ",
        demoComponent: "terminal-demo"
      },
      {
        id: "step2",
        title: "2. Tailwind プラグインの有効化",
        description: "<code>vite.config.ts</code> にプラグインを登録し、<code>style.css</code> の先頭でTailwindを読み込みます。",
        code: '/* style.css */\n@import "tailwindcss";',
        insightLevel: "CSSレスの設計",
        insightText: "@import を一行書くだけで、これ以降は自分で独自のCSSファイルを触る必要がほぼなくなります。デザインは全てHTMLのクラスとして完結させるのがモダンなアプローチです。",
        demoTitle: "エディタ設定イメージ",
        demoComponent: "editor-demo"
      }
    ]
  },
  {
    chapterTitle: "第2章：Tailwindの哲学、コツ",
    chapterDescription: "美しいUIを組み上げるための「法則」と「設計思想」を学びます。",
    steps: [
      {
        id: "step3",
        title: "3. ユーティリティファーストの哲学",
        description: "Webページを作るには <b>HTML（骨組み）</b> と <b>CSS（デザイン）</b> を使います。<br>通常、CSSは別のファイルに複雑なルールを書きますが、Tailwindは「あらかじめ用意されたタグ（ユーティリティクラス）」をパズルのようにHTMLに直接くっつけてデザインを作ります。",
        insightLevel: "中級者向けの視点（設計思想）",
        insightText: "なぜTailwindを使うと洗練されるのか？それはシステムが事前に色やサイズの「美しい制限（スケール）」を持っているため、開発者が自由に設定しすぎてデザインが破綻するのを防ぐからです。",
        demoTitle: "イメージ図",
        demoComponent: "step1-demo"
      },
      {
        id: "step4",
        title: "4. 空間の支配 (PaddingとMargin)",
        description: "デザインを綺麗に見せるには「余白（空白）」がとても大事です。<br><br>・<b>Padding (`p-4` など)</b>: 箱の「内側」のクッション。<br>・<b>Margin (`m-4` など)</b>: 箱の「外側」のバリア（距離）。",
        insightLevel: "中級者向けの視点（コツ）",
        insightText: "余白はデザインの命です。Tailwindの余白クラスは基本的に `1` = `0.25rem`（約4px）に設計されています。UIを組む時は「8px（クラスの数値2の倍数）」で間隔を統一すると、画面全体に美しいリズムが生まれます。",
        demoTitle: "箱（Box）の図解",
        demoComponent: "step3-demo"
      },
      {
        id: "step5",
        title: "5. 要素のグループ化と空間 (Gapの魔法)",
        description: "複数並べる時は <code>flex</code> と <code>gap</code> を使います。ここで重要なのが「余白の距離＝それぞれの関係性の強さ」というルールです。",
        code: '<div class="flex flex-col gap-2">\n  <p>近い要素</p>\n  <p>（グループになる）</p>\n</div>',
        insightLevel: "中級者向けの視点（近接の法則）",
        insightText: "人間の脳は「近くにあるものを1つのグループ」として無意識に認識します。画像と見出しと説明文は狭く（gap-2 等）、別のカード・セクション同士は広く（gap-8 等）とることで、直感的に伝わる「情報のまとまり」を作ることができます。これをゲシュタルト要因の「近接」と呼びます。",
        demoTitle: "均等な余白 vs グルーピングした余白",
        demoComponent: "step-proximity-demo"
      },
      {
        id: "step6",
        title: "6. タイポグラフィと色彩心理",
        description: "色と大きさを変えてみましょう。例えば文字を白くするなら `text-white`、サイズを大きくするなら `text-2xl` と書きます。英語の意味の通りに機能します。",
        code: '<p class="text-stone-300 text-2xl font-bold">\n  Nordic Dark World\n</p>',
        insightLevel: "中級者向けの視点（美しさの本質）",
        insightText: "ダークテーマにおいて「本当に真っ黒（#000000）」や「真っ白（#FFFFFF）」を多用すると、コントラストが強すぎて目が疲れます。背景に `neutral-900` のような深みのあるグレーを、文字には真っ白ではない `stone-300` などを選ぶのが「Nordic Dark（北欧ダーク）」の極意です。",
        demoTitle: "色のプレビュー",
        demoComponent: "step2-demo"
      },
      {
        id: "step7",
        title: "7. 質感の構築 (角丸・ボーダー・影)",
        description: "現在流行しているアプリの多くは、少し角を丸くして、浮いているような立体感を持っています。これだけで「硬い四角」が「モダンなカード」に変わります。",
        code: '<div class="rounded-2xl border border-white/10 shadow-xl">\n  カード\n</div>',
        insightLevel: "中級者向けの視点（設計思想）",
        insightText: "暗い背景での「影（shadow）」は同化して見えにくいため、ダークテーマではわずかに光を反射しているように見せる「薄いボーダー（`border-white/10` など）」を描き、要素の輪郭（エッジ）を際立たせるテクニックが非常に重要です。",
        demoTitle: "質感の比較",
        demoComponent: "step4-demo"
      },
      {
        id: "step8",
        title: "8. 心地よいインタラクション",
        description: "ボタンの上にマウスを乗せた時（ホバー）や、クリックした時の動きを設定します。Tailwindでは `hover:色` とするだけで、触れることができるようになります。",
        code: '<button class="transition-all hover:bg-white active:scale-95">\n  ボタン\n</button>',
        insightLevel: "中級者向けの視点（コツ）",
        insightText: "ユーザーの操作に対する「わずかなアニメーション（`transition-all`）」と「押した感覚（`active:scale-95`）」は、即座にフィードバックを返すことでシステムへの安心感と上質さを大幅に引き立てます。",
        demoTitle: "アニメーションがないUIとあるUI",
        demoComponent: "step-interaction-demo"
      }
    ]
  },
  {
    chapterTitle: "第3章：よくあるUIパーツの具体例 (Nordic Dark)",
    chapterDescription: "これまでの法則を活用し、上質な具体的なUIパーツを自作してみましょう。",
    steps: [
      {
        id: "step9",
        title: "9. Primary Button の構築",
        description: "一番目立たせるべきボタンを作ります。ポイントは『真っ白ではなく石のような白（stone-100）』を使うことです。",
        code: '<button class="px-8 py-3 bg-stone-100 text-neutral-900 font-bold rounded-full transition-all hover:bg-white active:scale-95 shadow-xl shadow-white/5 text-sm">\n  Primary Action\n</button>',
        insightLevel: "設計思想",
        insightText: "アクション全体の中で最も視線を誘導したい箇所（保存、次へ進む等）にのみ、この強いコントラストを持つソリッドボタンを使用します。",
        demoTitle: "プレビュー",
        demoComponent: "practice-btn"
      },
      {
        id: "step10",
        title: "10. Status Badge (ステータスバッジ) の構築",
        description: "「完了」「処理中」などを控えめに示す小さなバッジです。背景色を透過（`/10` などの不透明度）させることがコツです。",
        code: '<span class="px-3 py-1 bg-emerald-500/10 text-emerald-400 border border-emerald-500/20 rounded-full text-xs font-bold tracking-wide">\n  Success\n</span>',
        insightLevel: "設計思想",
        insightText: "原色をベタ塗りすると目立ちすぎてしまうため、文字色・背景色・枠線を全て『同じ色相（emeraldなど）』に揃えつつ、透明度を変えてなじませるのがモダンUIの基本形です。",
        demoTitle: "プレビュー",
        demoComponent: "practice-badge"
      },
      {
        id: "step11",
        title: "11. Container Card (コンテナカード) の構築",
        description: "情報を美しく包み込む箱です。背景を他の要素よりもわずかに浮き上がらせ（明るくし）、薄いボーダーで仕切ることで情報の独立性を高めます。",
        code: '<div class="p-6 bg-[#1A1A1A] border border-neutral-800 rounded-[2rem] hover:border-neutral-700 transition-colors shadow-lg">\n  <h3 class="text-xl font-bold text-stone-100 mb-2">Nordic Card</h3>\n  <p class="text-neutral-400 text-sm">美しい余白と細い境界線がもたらす情報整理。</p>\n</div>',
        insightLevel: "設計思想",
        insightText: "ただの箱ではなく、情報をグループ化し、見出し（白）と説明文（グレー）という文字の対比によって読者にストレスを与えずに視線を誘導します。",
        demoTitle: "プレビュー",
        demoComponent: "practice-card"
      }
    ]
  }
];
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
      <nav class="flex items-center gap-6 md:gap-12 border-b border-neutral-800 mb-16 relative overflow-x-auto whitespace-nowrap hide-scrollbar">
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
        <button
          @click="activeTab = 'tutorial'"
          :class="['pb-5 text-sm font-bold tracking-wider transition-all duration-300 border-b-2 z-10 flex items-center gap-2', activeTab === 'tutorial' ? 'border-emerald-400 text-emerald-400' : 'border-transparent text-neutral-600 hover:text-neutral-400']"
        >
          <svg xmlns="http://www.w3.org/2000/svg" class="w-4 h-4" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round"><path d="M12 2v20"/><path d="M17 5H9.5a3.5 3.5 0 0 0 0 7h5a3.5 3.5 0 0 1 0 7H6"/></svg>
          Tailwind Beginner (初心者向け)
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
                  <div class="flex flex-col h-full bg-[#1A1A1A] border border-neutral-800/80 rounded-[2rem] p-6 hover:border-neutral-700 transition-colors shadow-lg">
                    <div class="flex items-center gap-3 mb-6">
                      <span class="text-neutral-600 font-mono text-xs opacity-50">0{{ index + 1 }}</span>
                      <h3 class="text-xl font-bold text-stone-100 tracking-tight group-hover:text-white transition-colors truncate">{{ item.name }}</h3>
                    </div>

                    <div class="w-full aspect-[4/3] bg-[#121212] border border-neutral-800/50 rounded-2xl flex flex-col items-center justify-center relative overflow-hidden shadow-inner mb-8 group-hover:bg-[#151515] transition-colors">
                      <div class="absolute inset-0 opacity-[0.03] pointer-events-none bg-[radial-gradient(#e5e7eb_1px,transparent_1px)] [background-size:16px_16px]"></div>
                      
                      <!-- Default App Renderings (Omitted to keep it exactly identical to previous implementation for General tab) -->
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

                    <div class="mb-6 flex-1">
                      <div class="text-[8px] font-black uppercase tracking-widest text-neutral-600 mb-2 border-l-2 border-neutral-700 pl-2">Design Logic</div>
                      <p class="text-neutral-400 text-sm leading-relaxed font-medium">{{ item.description }}</p>
                    </div>

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

          <!-- Tutorial Tab: Nordic Dark & Beginners -->
          <div v-else-if="activeTab === 'tutorial'" key="tutorial" class="max-w-4xl mx-auto flex flex-col gap-12 pb-20">
            <div class="text-center mb-8">
              <h2 class="text-4xl md:text-5xl font-extrabold text-emerald-400 mb-6 tracking-tight">UI Build Tutorial</h2>
              <p class="text-neutral-400 text-lg md:text-xl leading-relaxed max-w-2xl mx-auto">
                「Nordic Dark（北欧ダークテーマ）」の上質なUIはどうやって作られているのか？<br>
                Tailwindの基礎知識から、プロも使う設計思想までを体験しながら学びましょう。
              </p>
            </div>

            
            <!-- Chapters Loop -->
            <div v-for="(chapter, cIndex) in tutorialChapters" :key="'chap'+cIndex" class="mb-24">
              <!-- Chapter Title -->
              <div class="mb-12 border-b border-neutral-800 pb-6 relative">
                <div class="absolute -left-8 top-1/2 -translate-y-1/2 w-4 h-[2px] bg-emerald-400 opacity-50 hidden md:block"></div>
                <h3 class="text-3xl font-extrabold text-stone-100 mb-3">{{ chapter.chapterTitle }}</h3>
                <p class="text-neutral-400 text-base md:text-lg">{{ chapter.chapterDescription }}</p>
              </div>

              <!-- Tutorial Steps -->
              <div class="flex flex-col gap-12">
                <div v-for="step in chapter.steps" :key="step.id" class="bg-[#1A1A1A] border border-neutral-800 rounded-[2rem] p-8 md:p-12 shadow-2xl relative overflow-hidden group hover:border-neutral-700 transition-colors duration-500">
                  
                  <div class="absolute -top-4 -right-4 text-[120px] font-black text-white/[0.02] leading-none select-none pointer-events-none transition-transform duration-700 group-hover:scale-110">
                    {{ step.title.split('.')[0] }}
                  </div>

                  <h3 class="text-2xl md:text-3xl font-bold text-stone-100 mb-6 relative z-10">
                    {{ step.title }}
                  </h3>
                  
                  <p class="text-neutral-300 text-base md:text-lg leading-relaxed mb-6 font-medium relative z-10" v-html="step.description"></p>

                  <div v-if="step.insightText" class="mb-10 bg-emerald-500/5 border border-emerald-500/20 rounded-2xl p-5 relative z-10 flex gap-4 text-emerald-100 text-sm">
                    <svg xmlns="http://www.w3.org/2000/svg" class="w-6 h-6 text-emerald-400 shrink-0" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 16h-1v-4h-1m1-4h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z" /></svg>
                    <div>
                      <div class="font-bold text-emerald-400 mb-1 text-xs uppercase tracking-widest">{{ step.insightLevel }}</div>
                      <p class="leading-relaxed opacity-90 font-mono">{{ step.insightText }}</p>
                    </div>
                  </div>

                  <div v-if="step.code" class="bg-[#121212] rounded-2xl p-6 mb-10 border border-neutral-800 relative z-10 overflow-x-auto">
                    <div class="flex items-center gap-2 mb-4">
                      <span class="w-3 h-3 rounded-full bg-red-500/80"></span>
                      <span class="w-3 h-3 rounded-full bg-amber-500/80"></span>
                      <span class="w-3 h-3 rounded-full bg-green-500/80"></span>
                      <span class="text-xs font-mono text-neutral-500 ml-2">Tailwind Code</span>
                    </div>
                    <pre class="text-stone-300 font-mono text-sm leading-relaxed whitespace-pre-wrap">{{ step.code }}</pre>
                  </div>

                  <div class="relative z-10">
                    <div class="text-[10px] font-black uppercase tracking-widest text-emerald-400/70 mb-3 border-l-2 border-emerald-500/50 pl-2">{{ step.demoTitle }}</div>
                    <div class="w-full bg-[#121212] border border-neutral-800 rounded-2xl p-8 md:p-12 mb-4 flex flex-col items-center justify-center min-h-[200px] overflow-hidden">
                      
                      <template v-if="step.demoComponent === 'terminal-demo'">
                        <div class="w-full max-w-lg bg-neutral-900 border border-neutral-800 rounded-xl overflow-hidden shadow-2xl text-left">
                          <div class="bg-neutral-800/80 px-4 py-3 flex items-center gap-2 border-b border-neutral-700/50">
                            <div class="w-3 h-3 rounded-full bg-red-500/80"></div>
                            <div class="w-3 h-3 rounded-full bg-amber-500/80"></div>
                            <div class="w-3 h-3 rounded-full bg-green-500/80"></div>
                            <span class="text-[10px] text-neutral-400 ml-4 font-mono font-bold tracking-widest uppercase">bash</span>
                          </div>
                          <div class="p-6 font-mono text-sm leading-relaxed text-stone-300">
                            <span class="text-emerald-400 font-bold">➜</span> <span class="text-stone-100 font-bold">~</span> <span class="text-neutral-400">npm create</span> <span class="text-stone-300">vite@latest my-project</span><br>
                            <span class="text-emerald-400 font-bold">➜</span> <span class="text-stone-100 font-bold">my-project</span> <span class="text-neutral-400">npm install</span> <span class="text-stone-300">tailwindcss @tailwindcss/vite</span><br>
                            <span class="text-emerald-400">✔</span> <span class="text-stone-400">Packages installed successfully.</span>
                          </div>
                        </div>
                      </template>

                      <template v-if="step.demoComponent === 'editor-demo'">
                        <div class="w-full max-w-lg bg-[#111111] border border-neutral-800 rounded-xl overflow-hidden shadow-2xl text-left font-mono">
                          <div class="flex items-center text-xs text-neutral-500 bg-neutral-900/80">
                            <div class="px-5 py-2.5 border-r border-neutral-800">vite.config.ts</div>
                            <div class="px-5 py-2.5 bg-neutral-800/30 text-emerald-400 border-t-2 border-emerald-400">style.css</div>
                          </div>
                          <div class="p-6 text-sm leading-relaxed">
                            <span class="text-stone-500 italic">/* Tailwindのコア機能の読み込む */</span><br>
                            <span class="text-emerald-400">@import</span> <span class="text-stone-300">"tailwindcss"</span>;<br><br>
                            <span class="text-stone-500 italic">/* 独自のCSSは書かずに終わります */</span>
                          </div>
                        </div>
                      </template>

                      <template v-if="step.demoComponent === 'step1-demo'">
                        <div class="flex flex-col md:flex-row items-center gap-8 text-center text-sm font-bold text-neutral-400">
                          <div class="flex flex-col items-center gap-4">
                            <div class="w-20 h-20 border-4 border-dashed border-neutral-600 flex items-center justify-center rounded-xl">
                              HTML
                            </div>
                            <span>構造のみの<br>「骨組み」</span>
                          </div>
                          <span class="text-3xl text-neutral-600">＋</span>
                          <div class="flex flex-col items-center gap-4">
                            <div class="w-24 h-20 bg-neutral-800 flex items-center justify-center rounded-xl shadow-lg border border-neutral-700 text-xs gap-1 flex-wrap p-2 text-emerald-400">
                              <span>p-4</span><span>flex</span><span>bg-dark</span><span>rounded</span>
                            </div>
                            <span>無数の便利な<br>「ユーティリティ」</span>
                          </div>
                          <span class="text-3xl text-neutral-600">＝</span>
                          <div class="flex flex-col items-center gap-4">
                            <div class="px-6 py-3 bg-stone-100 text-neutral-900 rounded-full font-bold shadow-xl">
                              Nordic Button
                            </div>
                            <span>洗練された<br>UIコンポーネント</span>
                          </div>
                        </div>
                      </template>

                      <template v-if="step.demoComponent === 'step2-demo'">
                        <div class="flex flex-col items-center gap-8 w-full max-w-sm text-center">
                          <div class="p-6 bg-black text-white w-full border border-red-500/30">
                            <h4 class="text-xl font-bold mb-2">#000000 & #FFFFFF</h4>
                            <p class="text-xs">コントラストが強すぎて長時間見ると目が疲れる、よくあるダークモード表現。</p>
                          </div>
                          <div class="p-6 bg-neutral-900 text-stone-300 w-full border border-emerald-500/30 rounded-2xl shadow-xl">
                            <h4 class="text-xl font-bold mb-2 text-stone-100">Nordic Dark</h4>
                            <p class="text-sm">背景は深いグレー、文字は温かみのあるストーン。上質で目に優しい美しさ。</p>
                          </div>
                        </div>
                      </template>

                      <template v-if="step.demoComponent === 'step3-demo'">
                        <div class="relative w-64 h-64 border border-blue-500/30 rounded-xl bg-blue-500/5 flex flex-col items-center justify-center">
                          <div class="absolute -top-6 text-blue-400 font-mono text-xs font-bold">↑ Margin (m-8 : 要素間の距離)</div>
                          <div class="w-48 h-48 border-2 border-emerald-500 rounded-2xl bg-emerald-500/20 flex flex-col items-center justify-center relative">
                            <div class="absolute top-3 text-emerald-300 font-mono text-xs font-bold">Padding (p-6)</div>
                            <div class="w-32 h-32 bg-stone-200 rounded-xl text-neutral-900 font-bold flex flex-col items-center justify-center text-sm px-4 text-center">
                              ゆとりのある<br>コンテンツ領域
                            </div>
                          </div>
                        </div>
                      </template>

                      <template v-if="step.demoComponent === 'step-proximity-demo'">
                        <div class="flex flex-col md:flex-row gap-8 w-full items-center justify-center text-left">
                          <div class="flex-1 bg-black p-6 rounded-2xl border border-red-500/30 flex flex-col w-full max-w-sm shrink-0">
                            <div class="text-[10px] font-bold text-red-400 mb-4 tracking-widest text-center opacity-80">BAD (均等な余白)</div>
                            <div class="w-full flex-col flex space-y-6">
                               <div class="w-12 h-12 bg-neutral-800 rounded-lg"></div>
                               <div class="h-3 bg-neutral-700 rounded w-1/2"></div>
                               <div class="h-2 bg-neutral-800 rounded w-full"></div>
                               <div class="w-12 h-12 bg-neutral-800 rounded-lg"></div>
                               <div class="h-3 bg-neutral-700 rounded w-1/2"></div>
                               <div class="h-2 bg-neutral-800 rounded w-full"></div>
                            </div>
                          </div>
                          <div class="flex-1 bg-neutral-900 border border-emerald-500/30 shadow-2xl rounded-[2rem] p-6 flex flex-col w-full max-w-sm relative">
                            <div class="text-[10px] font-bold text-emerald-400 mb-4 tracking-widest text-center">GOOD (グルーピング)</div>
                            <div class="w-full flex-col flex gap-8">
                               <div class="flex flex-col gap-3 p-3 bg-white/5 rounded-xl border border-white/5">
                                 <div class="w-12 h-12 bg-neutral-700 rounded-lg"></div>
                                 <div class="h-3 bg-stone-300 rounded w-1/2"></div>
                                 <div class="h-2 bg-neutral-600 rounded w-full"></div>
                               </div>
                               <div class="flex flex-col gap-3 p-3 bg-white/5 rounded-xl border border-white/5">
                                 <div class="w-12 h-12 bg-neutral-700 rounded-lg"></div>
                                 <div class="h-3 bg-stone-300 rounded w-1/2"></div>
                                 <div class="h-2 bg-neutral-600 rounded w-full"></div>
                               </div>
                            </div>
                          </div>
                        </div>
                      </template>

                      <template v-if="step.demoComponent === 'step4-demo'">
                        <div class="flex flex-col sm:flex-row gap-12 items-center justify-center w-full">
                          <div class="w-40 h-40 bg-neutral-800 flex items-center justify-center text-stone-300 font-bold text-center text-sm">
                            border無し<br>shadow無し<br>角丸無し
                          </div>
                          <svg xmlns="http://www.w3.org/2000/svg" class="w-6 h-6 text-neutral-600" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M14 5l7 7m0 0l-7 7m7-7H3" /></svg>
                          <div class="w-40 h-40 bg-[#1A1A1A] rounded-[2rem] shadow-2xl flex items-center justify-center text-stone-100 font-bold text-center text-sm border border-neutral-700 relative overflow-hidden">
                            <div class="absolute inset-0 opacity-[0.03] pointer-events-none bg-[radial-gradient(#e5e7eb_1px,transparent_1px)] [background-size:16px_16px]"></div>
                            モダンな<br>浮遊感と輪郭
                          </div>
                        </div>
                      </template>

                      <template v-if="step.demoComponent === 'step-interaction-demo'">
                        <div class="flex gap-8 items-center">
                          <button class="bg-neutral-800 text-stone-300 px-6 py-3 rounded-lg border border-neutral-700">
                            フィードバックなし
                          </button>
                          <button class="bg-neutral-800 text-stone-300 px-6 py-3 rounded-lg border border-neutral-700 transition-all duration-300 hover:bg-neutral-700 hover:text-white hover:border-neutral-500 active:scale-95 shadow-lg hover:shadow-xl">
                            触感のある動き
                          </button>
                        </div>
                      </template>

                      <template v-if="step.demoComponent === 'practice-btn'">
                        <button class="px-8 py-3 bg-stone-100 text-neutral-900 font-bold rounded-full transition-all hover:bg-white active:scale-95 shadow-xl shadow-white/5 text-sm">
                          Primary Action
                        </button>
                      </template>

                      <template v-if="step.demoComponent === 'practice-badge'">
                        <span class="px-3 py-1 bg-emerald-500/10 text-emerald-400 border border-emerald-500/20 rounded-full text-xs font-bold tracking-wide">
                          Success
                        </span>
                      </template>

                      <template v-if="step.demoComponent === 'practice-card'">
                        <div class="p-6 bg-[#1A1A1A] border border-neutral-800 rounded-[2rem] hover:border-neutral-700 transition-colors shadow-lg max-w-sm w-full text-left cursor-default">
                          <h3 class="text-xl font-bold text-stone-100 mb-2">Nordic Card</h3>
                          <p class="text-neutral-400 text-sm leading-relaxed">美しい余白と細い境界線がもたらす情報整理。これがNordic DarkなUIコンポーネント開発の極意です。</p>
                        </div>
                      </template>

                    </div>
                  </div>
                </div>
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

/* Hide scrollbar for tabs on mobile */
.hide-scrollbar::-webkit-scrollbar {
  display: none;
}
.hide-scrollbar {
  -ms-overflow-style: none;
  scrollbar-width: none;
}
</style>
