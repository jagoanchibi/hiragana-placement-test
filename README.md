<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Baca Hiragana</title>
<style>
@import url('https://fonts.googleapis.com/css2?family=Noto+Sans+JP:wght@300;400;700&family=DM+Sans:wght@300;400;500;600;700&display=swap');

:root {
  --bg: #faf7f2;
  --paper: #ffffff;
  --ink: #1c1c24;
  --muted: #8a8a9a;
  --border: #e8e4dc;
  --accent: #c0392b;
  --accent2: #2e6da4;
  --green: #2d8a5e;
  --surface: #f4f1ec;
  --tag-bg: #eee9e0;
}

* { box-sizing: border-box; margin: 0; padding: 0; }

body {
  font-family: 'DM Sans', sans-serif;
  background: var(--bg);
  color: var(--ink);
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 0 16px 60px;
}

/* ── HEADER ── */
header {
  width: 100%;
  max-width: 680px;
  padding: 28px 0 20px;
  display: flex;
  align-items: flex-end;
  justify-content: space-between;
}

.site-title {
  font-family: 'Noto Sans JP', sans-serif;
  font-size: 20px;
  font-weight: 400;
  letter-spacing: 3px;
  color: var(--ink);
}

.site-title em {
  font-style: normal;
  color: var(--accent);
}

.header-sub {
  font-size: 12px;
  color: var(--muted);
}

/* ── LEVEL TABS ── */
.level-tabs {
  width: 100%;
  max-width: 680px;
  display: flex;
  gap: 6px;
  margin-bottom: 20px;
  overflow-x: auto;
  scrollbar-width: none;
}
.level-tabs::-webkit-scrollbar { display: none; }

.level-btn {
  padding: 8px 18px;
  border-radius: 20px;
  border: 1.5px solid var(--border);
  background: var(--paper);
  color: var(--muted);
  font-size: 12px;
  font-weight: 600;
  cursor: pointer;
  white-space: nowrap;
  font-family: 'DM Sans', sans-serif;
  transition: all 0.2s;
}
.level-btn:hover { border-color: var(--accent2); color: var(--ink); }
.level-btn.active { background: var(--ink); border-color: var(--ink); color: white; }

/* ── STORY LIST ── */
.story-list {
  width: 100%;
  max-width: 680px;
  display: flex;
  flex-direction: column;
  gap: 10px;
  margin-bottom: 24px;
}

.story-card {
  background: var(--paper);
  border: 1.5px solid var(--border);
  border-radius: 14px;
  padding: 16px 20px;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: space-between;
  transition: all 0.2s;
}
.story-card:hover { border-color: var(--accent2); box-shadow: 0 2px 12px rgba(0,0,0,0.06); }
.story-card.active { border-color: var(--accent); background: rgba(192,57,43,0.03); }

.story-meta { flex: 1; }
.story-title-jp {
  font-family: 'Noto Sans JP', sans-serif;
  font-size: 18px;
  font-weight: 400;
  margin-bottom: 2px;
}
.story-title-id { font-size: 12px; color: var(--muted); }
.story-tags { display: flex; gap: 5px; margin-top: 6px; }
.tag {
  font-size: 10px;
  font-weight: 600;
  padding: 2px 8px;
  border-radius: 10px;
  background: var(--tag-bg);
  color: var(--muted);
  text-transform: uppercase;
  letter-spacing: 0.5px;
}
.tag.easy { background: rgba(45,138,94,0.1); color: var(--green); }
.tag.medium { background: rgba(46,109,164,0.1); color: var(--accent2); }
.tag.hard { background: rgba(192,57,43,0.1); color: var(--accent); }

.story-arrow { font-size: 18px; color: var(--border); transition: color 0.2s; }
.story-card:hover .story-arrow { color: var(--accent2); }

/* ── READING PANE ── */
.reading-pane {
  width: 100%;
  max-width: 680px;
  background: var(--paper);
  border: 1.5px solid var(--border);
  border-radius: 20px;
  padding: 32px 36px;
  display: none;
}
.reading-pane.show { display: block; }

.pane-header {
  display: flex;
  align-items: flex-start;
  justify-content: space-between;
  margin-bottom: 24px;
  gap: 12px;
}

.pane-titles {}
.pane-jp {
  font-family: 'Noto Sans JP', sans-serif;
  font-size: 22px;
  font-weight: 400;
  margin-bottom: 2px;
}
.pane-id { font-size: 13px; color: var(--muted); }

.pane-controls {
  display: flex;
  gap: 8px;
  flex-shrink: 0;
}

.ctrl-btn {
  padding: 7px 14px;
  border-radius: 20px;
  border: 1.5px solid var(--border);
  background: var(--surface);
  color: var(--ink);
  font-size: 12px;
  font-weight: 600;
  cursor: pointer;
  font-family: 'DM Sans', sans-serif;
  transition: all 0.2s;
  white-space: nowrap;
}
.ctrl-btn:hover { border-color: var(--ink); }
.ctrl-btn.on { background: var(--green); border-color: var(--green); color: white; }

/* ── TEXT BODY ── */
.text-body {
  font-family: 'Noto Sans JP', sans-serif;
  font-size: 22px;
  line-height: 2.8;
  color: var(--ink);
}

/* word wrapper */
.w {
  display: inline-block;
  position: relative;
  cursor: pointer;
  padding: 0 2px;
  border-radius: 4px;
  transition: background 0.15s;
  vertical-align: baseline;
}

.w:hover { background: rgba(46,109,164,0.08); }
.w.revealed { background: rgba(45,138,94,0.07); }

/* furigana above */
.furi {
  display: block;
  position: absolute;
  top: -1.1em;
  left: 50%;
  transform: translateX(-50%);
  font-family: 'DM Sans', sans-serif;
  font-size: 11px;
  font-weight: 600;
  color: var(--accent2);
  white-space: nowrap;
  pointer-events: none;
  opacity: 0;
  transition: opacity 0.2s;
  letter-spacing: 0.3px;
}

.w.revealed .furi,
.w:hover .furi { opacity: 1; }

/* show-all mode */
.text-body.show-all .furi { opacity: 1; }
.text-body.show-all .w { background: none; cursor: default; }

/* sentence break */
.sentence-break {
  display: block;
  height: 0;
  width: 100%;
}

/* ── MEANING STRIP ── */
.meaning-strip {
  margin-top: 24px;
  padding-top: 20px;
  border-top: 1.5px solid var(--border);
  display: flex;
  flex-direction: column;
  gap: 6px;
}

.meaning-label {
  font-size: 11px;
  text-transform: uppercase;
  letter-spacing: 1px;
  color: var(--muted);
  font-weight: 600;
}

.meaning-text {
  font-size: 14px;
  color: var(--ink);
  line-height: 1.7;
}

/* ── VOCAB TABLE ── */
.vocab-section {
  margin-top: 24px;
  padding-top: 20px;
  border-top: 1.5px solid var(--border);
}

.vocab-title {
  font-size: 11px;
  text-transform: uppercase;
  letter-spacing: 1px;
  color: var(--muted);
  font-weight: 600;
  margin-bottom: 12px;
}

.vocab-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(140px, 1fr));
  gap: 8px;
}

.vocab-item {
  background: var(--surface);
  border-radius: 10px;
  padding: 10px 12px;
}
.vocab-kana {
  font-family: 'Noto Sans JP', sans-serif;
  font-size: 18px;
  font-weight: 300;
  display: block;
  margin-bottom: 2px;
}
.vocab-roma { font-size: 11px; color: var(--accent2); font-weight: 600; }
.vocab-mean { font-size: 11px; color: var(--muted); margin-top: 1px; }

/* ── SCORE BAR ── */
.score-bar {
  margin-top: 20px;
  padding: 14px 16px;
  background: var(--surface);
  border-radius: 12px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 12px;
}
.score-info { font-size: 13px; color: var(--muted); }
.score-info strong { color: var(--ink); }
.score-track { flex: 1; height: 4px; background: var(--border); border-radius: 2px; overflow: hidden; }
.score-fill { height: 100%; background: var(--green); border-radius: 2px; transition: width 0.4s; }

/* ── NAV BETWEEN STORIES ── */
.pane-nav {
  display: flex;
  justify-content: space-between;
  margin-top: 24px;
  padding-top: 20px;
  border-top: 1.5px solid var(--border);
}
.nav-btn {
  padding: 10px 20px;
  border-radius: 20px;
  border: 1.5px solid var(--border);
  background: var(--surface);
  font-size: 13px;
  font-weight: 600;
  cursor: pointer;
  font-family: 'DM Sans', sans-serif;
  color: var(--ink);
  transition: all 0.2s;
}
.nav-btn:hover { border-color: var(--ink); }
.nav-btn:disabled { opacity: 0.3; cursor: default; }

@media (max-width: 520px) {
  .reading-pane { padding: 24px 20px; }
  .text-body { font-size: 20px; }
}
</style>
</head>
<body>

<header>
  <div>
    <div class="site-title">よむ<em>練習</em></div>
    <div class="header-sub" style="margin-top:3px">Latihan Membaca Hiragana</div>
  </div>
  <div class="header-sub">Klik kata untuk lihat bacaan</div>
</header>

<!-- Level filter -->
<div class="level-tabs" id="level-tabs"></div>

<!-- Story list -->
<div class="story-list" id="story-list"></div>

<!-- Reading pane -->
<div class="reading-pane" id="reading-pane">
  <div class="pane-header">
    <div class="pane-titles">
      <div class="pane-jp" id="pane-jp"></div>
      <div class="pane-id" id="pane-id"></div>
    </div>
    <div class="pane-controls">
      <button class="ctrl-btn" id="btn-reveal-all" onclick="toggleRevealAll()">Tampilkan Semua</button>
      <button class="ctrl-btn" id="btn-reset-reveal" onclick="resetReveals()">Reset</button>
    </div>
  </div>

  <div class="text-body" id="text-body"></div>

  <div class="score-bar">
    <div class="score-info">Kata terungkap: <strong id="score-revealed">0</strong> / <strong id="score-total">0</strong></div>
    <div class="score-track"><div class="score-fill" id="score-fill" style="width:0%"></div></div>
  </div>

  <div class="meaning-strip">
    <div class="meaning-label">Terjemahan</div>
    <div class="meaning-text" id="meaning-text"></div>
  </div>

  <div class="vocab-section">
    <div class="vocab-title">Kosakata Penting</div>
    <div class="vocab-grid" id="vocab-grid"></div>
  </div>

  <div class="pane-nav">
    <button class="nav-btn" id="btn-prev" onclick="navStory(-1)">← Sebelumnya</button>
    <button class="nav-btn" id="btn-next" onclick="navStory(1)">Selanjutnya →</button>
  </div>
</div>

<script>
// ══════════════════════════════════════
// STORIES DATA
// ══════════════════════════════════════
// Each sentence: array of {kana, romaji, space?}
// space=true adds a visual space after (for particle/word separation)

const stories = [
  // ────────────────────────────────────
  // MUDAH
  // ────────────────────────────────────
  {
    id: 0,
    level: "Mudah",
    titleJP: "いぬ と ねこ",
    titleID: "Anjing dan Kucing",
    translation: "Ada seekor anjing. Ada juga seekor kucing. Anjing itu putih. Kucing itu hitam. Keduanya berteman baik.",
    vocab: [
      {kana:"いぬ", romaji:"inu", mean:"anjing"},
      {kana:"ねこ", romaji:"neko", mean:"kucing"},
      {kana:"しろい", romaji:"shiroi", mean:"putih"},
      {kana:"くろい", romaji:"kuroi", mean:"hitam"},
      {kana:"ともだち", romaji:"tomodachi", mean:"teman"},
    ],
    sentences: [
      [
        {k:"いぬ",r:"inu",sp:true},{k:"が",r:"ga",sp:true},{k:"います",r:"imasu",sp:false},{k:"。",r:""}
      ],
      [
        {k:"ねこ",r:"neko",sp:true},{k:"も",r:"mo",sp:true},{k:"います",r:"imasu",sp:false},{k:"。",r:""}
      ],
      [
        {k:"いぬ",r:"inu",sp:true},{k:"は",r:"wa",sp:true},{k:"しろい",r:"shiroi",sp:1},{k:"です",r:"desu",sp:false},{k:"。",r:""}
      ],
      [
        {k:"ねこ",r:"neko",sp:true},{k:"は",r:"wa",sp:true},{k:"くろい",r:"kuroi",sp:true},{k:"です",r:"desu",sp:false},{k:"。",r:""}
      ],
      [
        {k:"ふたり",r:"futari",sp:true},{k:"は",r:"wa",sp:true},{k:"ともだち",r:"tomodachi",sp:true},{k:"です",r:"desu",sp:false},{k:"。",r:""}
      ],
    ]
  },

  {
    id: 1,
    level: "Mudah",
    titleJP: "あさごはん",
    titleID: "Sarapan",
    translation: "Pagi hari, saya makan nasi. Saya juga minum teh. Enak sekali. Saya pergi ke sekolah.",
    vocab: [
      {kana:"あさ", romaji:"asa", mean:"pagi"},
      {kana:"ごはん", romaji:"gohan", mean:"nasi"},
      {kana:"おちゃ", romaji:"ocha", mean:"teh"},
      {kana:"おいしい", romaji:"oishii", mean:"enak"},
      {kana:"がっこう", romaji:"gakkou", mean:"sekolah"},
    ],
    sentences: [
      [
        {k:"あさ",r:"asa",sp:true},{k:"に",r:"ni",sp:true},{k:"ごはん",r:"gohan",sp:true},{k:"を",r:"wo",sp:true},{k:"たべます",r:"tabemasu",sp:false},{k:"。",r:""}
      ],
      [
        {k:"おちゃ",r:"ocha",sp:true},{k:"も",r:"mo",sp:true},{k:"のみます",r:"nomimasu",sp:false},{k:"。",r:""}
      ],
      [
        {k:"とても",r:"totemo",sp:true},{k:"おいしい",r:"oishii",sp:true},{k:"です",r:"desu",sp:false},{k:"。",r:""}
      ],
      [
        {k:"がっこう",r:"gakkou",sp:true},{k:"へ",r:"e",sp:true},{k:"いきます",r:"ikimasu",sp:false},{k:"。",r:""}
      ],
    ]
  },

  {
    id: 2,
    level: "Mudah",
    titleJP: "わたしの へや",
    titleID: "Kamarku",
    translation: "Ini adalah kamarku. Ada meja dan kursi. Di meja ada buku. Buku itu merah. Saya suka kamar ini.",
    vocab: [
      {kana:"へや", romaji:"heya", mean:"kamar"},
      {kana:"つくえ", romaji:"tsukue", mean:"meja"},
      {kana:"いす", romaji:"isu", mean:"kursi"},
      {kana:"ほん", romaji:"hon", mean:"buku"},
      {kana:"あかい", romaji:"akai", mean:"merah"},
    ],
    sentences: [
      [
        {k:"これ",r:"kore",sp:true},{k:"は",r:"wa",sp:true},{k:"わたし",r:"watashi",sp:true},{k:"の",r:"no",sp:true},{k:"へや",r:"heya",sp:true},{k:"です",r:"desu",sp:false},{k:"。",r:""}
      ],
      [
        {k:"つくえ",r:"tsukue",sp:true},{k:"と",r:"to",sp:true},{k:"いす",r:"isu",sp:true},{k:"が",r:"ga",sp:true},{k:"あります",r:"arimasu",sp:false},{k:"。",r:""}
      ],
      [
        {k:"つくえ",r:"tsukue",sp:true},{k:"の",r:"no",sp:true},{k:"うえ",r:"ue",sp:true},{k:"に",r:"ni",sp:true},{k:"ほん",r:"hon",sp:true},{k:"が",r:"ga",sp:true},{k:"あります",r:"arimasu",sp:false},{k:"。",r:""}
      ],
      [
        {k:"ほん",r:"hon",sp:true},{k:"は",r:"wa",sp:true},{k:"あかい",r:"akai",sp:true},{k:"です",r:"desu",sp:false},{k:"。",r:""}
      ],
      [
        {k:"わたし",r:"watashi",sp:true},{k:"は",r:"wa",sp:true},{k:"この",r:"kono",sp:true},{k:"へや",r:"heya",sp:true},{k:"が",r:"ga",sp:true},{k:"すき",r:"suki",sp:true},{k:"です",r:"desu",sp:false},{k:"。",r:""}
      ],
    ]
  },

  // ────────────────────────────────────
  // SEDANG
  // ────────────────────────────────────
  {
    id: 3,
    level: "Sedang",
    titleJP: "こうえんで",
    titleID: "Di Taman",
    translation: "Kemarin saya pergi ke taman. Cuacanya bagus. Ada banyak anak-anak bermain. Saya duduk di bangku dan membaca buku. Sangat menyenangkan.",
    vocab: [
      {kana:"こうえん", romaji:"kouen", mean:"taman"},
      {kana:"きのう", romaji:"kinou", mean:"kemarin"},
      {kana:"てんき", romaji:"tenki", mean:"cuaca"},
      {kana:"こども", romaji:"kodomo", mean:"anak-anak"},
      {kana:"ベンチ", romaji:"benchi", mean:"bangku"},
      {kana:"たのしい", romaji:"tanoshii", mean:"menyenangkan"},
    ],
    sentences: [
      [
        {k:"きのう",r:"kinou",sp:true},{k:"こうえん",r:"kouen",sp:true},{k:"へ",r:"e",sp:true},{k:"いきました",r:"ikimashita",sp:false},{k:"。",r:""}
      ],
      [
        {k:"てんき",r:"tenki",sp:true},{k:"が",r:"ga",sp:true},{k:"よかった",r:"yokatta",sp:true},{k:"です",r:"desu",sp:false},{k:"。",r:""}
      ],
      [
        {k:"こども",r:"kodomo",sp:true},{k:"たち",r:"tachi",sp:true},{k:"が",r:"ga",sp:true},{k:"たくさん",r:"takusan",sp:true},{k:"あそんで",r:"asonde",sp:true},{k:"いました",r:"imashita",sp:false},{k:"。",r:""}
      ],
      [
        {k:"わたし",r:"watashi",sp:true},{k:"は",r:"wa",sp:true},{k:"ベンチ",r:"benchi",sp:true},{k:"に",r:"ni",sp:true},{k:"すわって",r:"suwatte",sp:true},{k:"ほん",r:"hon",sp:true},{k:"を",r:"wo",sp:true},{k:"よみました",r:"yomimashita",sp:false},{k:"。",r:""}
      ],
      [
        {k:"とても",r:"totemo",sp:true},{k:"たのしかった",r:"tanoshikatta",sp:true},{k:"です",r:"desu",sp:false},{k:"。",r:""}
      ],
    ]
  },

  {
    id: 4,
    level: "Sedang",
    titleJP: "あめの ひ",
    titleID: "Hari Hujan",
    translation: "Hari ini hujan. Langit abu-abu dan gelap. Saya tidak bisa pergi keluar. Saya membuat teh panas di rumah. Sambil minum teh, saya mendengarkan musik. Hari yang tenang.",
    vocab: [
      {kana:"あめ", romaji:"ame", mean:"hujan"},
      {kana:"そら", romaji:"sora", mean:"langit"},
      {kana:"そと", romaji:"soto", mean:"luar"},
      {kana:"おんがく", romaji:"ongaku", mean:"musik"},
      {kana:"しずか", romaji:"shizuka", mean:"tenang"},
    ],
    sentences: [
      [
        {k:"きょう",r:"kyou",sp:true},{k:"は",r:"wa",sp:true},{k:"あめ",r:"ame",sp:true},{k:"です",r:"desu",sp:false},{k:"。",r:""}
      ],
      [
        {k:"そら",r:"sora",sp:true},{k:"は",r:"wa",sp:true},{k:"はいいろ",r:"haiiro",sp:true},{k:"で",r:"de",sp:true},{k:"くらい",r:"kurai",sp:true},{k:"です",r:"desu",sp:false},{k:"。",r:""}
      ],
      [
        {k:"そと",r:"soto",sp:true},{k:"へ",r:"e",sp:true},{k:"でかけられません",r:"dekakearemasen",sp:false},{k:"。",r:""}
      ],
      [
        {k:"いえ",r:"ie",sp:true},{k:"で",r:"de",sp:true},{k:"あついおちゃ",r:"atsui ocha",sp:true},{k:"を",r:"wo",sp:true},{k:"いれました",r:"iremashita",sp:false},{k:"。",r:""}
      ],
      [
        {k:"おちゃ",r:"ocha",sp:true},{k:"を",r:"wo",sp:true},{k:"のみながら",r:"nominagara",sp:true},{k:"おんがく",r:"ongaku",sp:true},{k:"を",r:"wo",sp:true},{k:"ききました",r:"kikimashita",sp:false},{k:"。",r:""}
      ],
      [
        {k:"しずかな",r:"shizukana",sp:true},{k:"いちにち",r:"ichinichi",sp:true},{k:"でした",r:"deshita",sp:false},{k:"。",r:""}
      ],
    ]
  },

  {
    id: 5,
    level: "Sedang",
    titleJP: "はじめての りょうり",
    titleID: "Memasak untuk Pertama Kali",
    translation: "Minggu lalu saya mencoba memasak sendiri untuk pertama kalinya. Saya membuat sup miso. Pertama, saya memotong sayuran. Kemudian saya memasak airnya. Rasanya agak aneh, tapi saya senang. Lain kali ingin mencoba lagi.",
    vocab: [
      {kana:"りょうり", romaji:"ryouri", mean:"memasak/masakan"},
      {kana:"みそしる", romaji:"misoshiru", mean:"sup miso"},
      {kana:"やさい", romaji:"yasai", mean:"sayuran"},
      {kana:"きる", romaji:"kiru", mean:"memotong"},
      {kana:"あじ", romaji:"aji", mean:"rasa"},
    ],
    sentences: [
      [
        {k:"せんしゅう",r:"senshuu",sp:true},{k:"はじめて",r:"hajimete",sp:true},{k:"ひとりで",r:"hitori de",sp:true},{k:"りょうり",r:"ryouri",sp:true},{k:"しました",r:"shimashita",sp:false},{k:"。",r:""}
      ],
      [
        {k:"みそしる",r:"misoshiru",sp:true},{k:"を",r:"wo",sp:true},{k:"つくりました",r:"tsukurimashita",sp:false},{k:"。",r:""}
      ],
      [
        {k:"まず",r:"mazu",sp:true},{k:"やさい",r:"yasai",sp:true},{k:"を",r:"wo",sp:true},{k:"きりました",r:"kirimashita",sp:false},{k:"。",r:""}
      ],
      [
        {k:"それから",r:"sorekara",sp:true},{k:"みず",r:"mizu",sp:true},{k:"を",r:"wo",sp:true},{k:"わかしました",r:"wakashimashita",sp:false},{k:"。",r:""}
      ],
      [
        {k:"あじ",r:"aji",sp:true},{k:"は",r:"wa",sp:true},{k:"すこし",r:"sukoshi",sp:true},{k:"へん",r:"hen",sp:true},{k:"でしたが",r:"deshita ga",sp:true},{k:"うれしかった",r:"ureshikatta",sp:true},{k:"です",r:"desu",sp:false},{k:"。",r:""}
      ],
      [
        {k:"つぎは",r:"tsugi wa",sp:true},{k:"また",r:"mata",sp:true},{k:"やってみたい",r:"yatte mitai",sp:true},{k:"です",r:"desu",sp:false},{k:"。",r:""}
      ],
    ]
  },

  // ────────────────────────────────────
  // SULIT
  // ────────────────────────────────────
  {
    id: 6,
    level: "Sulit",
    titleJP: "うみの きおく",
    titleID: "Kenangan Laut",
    translation: "Ketika saya masih kecil, setiap musim panas saya pergi ke laut bersama keluarga. Pasirnya putih dan airnya biru jernih. Saya berlari-lari di tepi pantai bersama kakak. Ibu membuat onigiri yang lezat. Sekarang kami sudah tinggal berpisah, tapi kenangan itu masih terasa nyata.",
    vocab: [
      {kana:"うみ", romaji:"umi", mean:"laut"},
      {kana:"なつ", romaji:"natsu", mean:"musim panas"},
      {kana:"かぞく", romaji:"kazoku", mean:"keluarga"},
      {kana:"すな", romaji:"suna", mean:"pasir"},
      {kana:"きおく", romaji:"kioku", mean:"kenangan"},
      {kana:"おにぎり", romaji:"onigiri", mean:"onigiri"},
    ],
    sentences: [
      [
        {k:"ちいさい",r:"chiisai",sp:true},{k:"ころ",r:"koro",sp:true},{k:"まいなつ",r:"mainatsu",sp:true},{k:"かぞく",r:"kazoku",sp:true},{k:"と",r:"to",sp:true},{k:"うみ",r:"umi",sp:true},{k:"へ",r:"e",sp:true},{k:"いきました",r:"ikimashita",sp:false},{k:"。",r:""}
      ],
      [
        {k:"すな",r:"suna",sp:true},{k:"は",r:"wa",sp:true},{k:"しろくて",r:"shirokute",sp:true},{k:"みず",r:"mizu",sp:true},{k:"は",r:"wa",sp:true},{k:"あおくて",r:"aokute",sp:true},{k:"きれい",r:"kirei",sp:true},{k:"でした",r:"deshita",sp:false},{k:"。",r:""}
      ],
      [
        {k:"あに",r:"ani",sp:true},{k:"と",r:"to",sp:true},{k:"いっしょに",r:"issho ni",sp:true},{k:"なぎさ",r:"nagisa",sp:true},{k:"を",r:"wo",sp:true},{k:"かけまわりました",r:"kakemawarimashita",sp:false},{k:"。",r:""}
      ],
      [
        {k:"はは",r:"haha",sp:true},{k:"は",r:"wa",sp:true},{k:"おいしい",r:"oishii",sp:true},{k:"おにぎり",r:"onigiri",sp:true},{k:"を",r:"wo",sp:true},{k:"つくって",r:"tsukutte",sp:true},{k:"くれました",r:"kuremashita",sp:false},{k:"。",r:""}
      ],
      [
        {k:"いまは",r:"ima wa",sp:true},{k:"はなれて",r:"hanarete",sp:true},{k:"すんでいますが",r:"sunde imasu ga",sp:true},{k:"あの",r:"ano",sp:true},{k:"きおく",r:"kioku",sp:true},{k:"は",r:"wa",sp:true},{k:"まだ",r:"mada",sp:true},{k:"なまなましい",r:"namanamashii",sp:true},{k:"です",r:"desu",sp:false},{k:"。",r:""}
      ],
    ]
  },

  {
    id: 7,
    level: "Sulit",
    titleJP: "としょかんの ひみつ",
    titleID: "Rahasia Perpustakaan",
    translation: "Di sudut perpustakaan tua itu ada sebuah rak tersembunyi. Buku-buku tua berdebu berjajar di sana. Suatu hari saya menemukan sebuah buku tanpa judul. Di dalamnya hanya ada satu kalimat: 'Yang kamu cari ada di dalam dirimu sendiri.' Sejak saat itu saya tidak bisa berhenti memikirkannya.",
    vocab: [
      {kana:"としょかん", romaji:"toshokan", mean:"perpustakaan"},
      {kana:"たな", romaji:"tana", mean:"rak"},
      {kana:"ふるい", romaji:"furui", mean:"tua/lama"},
      {kana:"ひみつ", romaji:"himitsu", mean:"rahasia"},
      {kana:"さがす", romaji:"sagasu", mean:"mencari"},
      {kana:"じぶん", romaji:"jibun", mean:"diri sendiri"},
    ],
    sentences: [
      [
        {k:"ふるい",r:"furui",sp:true},{k:"としょかん",r:"toshokan",sp:true},{k:"の",r:"no",sp:true},{k:"すみ",r:"sumi",sp:true},{k:"に",r:"ni",sp:true},{k:"かくれた",r:"kakureta",sp:true},{k:"たな",r:"tana",sp:true},{k:"が",r:"ga",sp:true},{k:"ありました",r:"arimashita",sp:false},{k:"。",r:""}
      ],
      [
        {k:"ほこりを",r:"hokori wo",sp:true},{k:"かぶった",r:"kabutta",sp:true},{k:"ふるい",r:"furui",sp:true},{k:"ほん",r:"hon",sp:true},{k:"が",r:"ga",sp:true},{k:"ならんでいました",r:"narande imashita",sp:false},{k:"。",r:""}
      ],
      [
        {k:"ある",r:"aru",sp:true},{k:"ひ",r:"hi",sp:true},{k:"だいめいの",r:"daimei no",sp:true},{k:"ない",r:"nai",sp:true},{k:"ほん",r:"hon",sp:true},{k:"を",r:"wo",sp:true},{k:"みつけました",r:"mitsukemashita",sp:false},{k:"。",r:""}
      ],
      [
        {k:"なかには",r:"naka ni wa",sp:true},{k:"いちぶん",r:"ichi bun",sp:true},{k:"だけ",r:"dake",sp:true},{k:"ありました",r:"arimashita",sp:false},{k:"：",r:""}
      ],
      [
        {k:"「さがしている",r:"\"sagashite iru",sp:true},{k:"ものは",r:"mono wa",sp:true},{k:"じぶんの",r:"jibun no",sp:true},{k:"なかに",r:"naka ni",sp:true},{k:"ある」",r:"aru\"",sp:false},{k:"。",r:""}
      ],
      [
        {k:"それ",r:"sore",sp:true},{k:"いらい",r:"irai",sp:true},{k:"かんがえつづけています",r:"kangae tsuzukete imasu",sp:false},{k:"。",r:""}
      ],
    ]
  },

  {
    id: 8,
    level: "Sulit",
    titleJP: "はるの おわり",
    titleID: "Akhir Musim Semi",
    translation: "Bunga sakura sudah mulai gugur. Kelopak-kelopaknya melayang di udara seperti salju. Saya berdiri sendirian di bawah pohon itu, menatap langit. Musim semi yang indah ini tidak akan bertahan lama. Justru karena itu, saya ingin mengingat saat ini selamanya.",
    vocab: [
      {kana:"さくら", romaji:"sakura", mean:"bunga sakura"},
      {kana:"はなびら", romaji:"hanabira", mean:"kelopak bunga"},
      {kana:"ゆき", romaji:"yuki", mean:"salju"},
      {kana:"そら", romaji:"sora", mean:"langit"},
      {kana:"おわり", romaji:"owari", mean:"akhir"},
      {kana:"きおく", romaji:"kioku", mean:"kenangan"},
    ],
    sentences: [
      [
        {k:"さくら",r:"sakura",sp:true},{k:"の",r:"no",sp:true},{k:"はなびら",r:"hanabira",sp:true},{k:"が",r:"ga",sp:true},{k:"ちりはじめました",r:"chiri hajimemashita",sp:false},{k:"。",r:""}
      ],
      [
        {k:"ゆき",r:"yuki",sp:true},{k:"のように",r:"no you ni",sp:true},{k:"はなびら",r:"hanabira",sp:true},{k:"が",r:"ga",sp:true},{k:"そらを",r:"sora wo",sp:true},{k:"まいました",r:"maimashita",sp:false},{k:"。",r:""}
      ],
      [
        {k:"わたしは",r:"watashi wa",sp:true},{k:"きのした",r:"ki no shita",sp:true},{k:"に",r:"ni",sp:true},{k:"ひとりで",r:"hitori de",sp:true},{k:"たって",r:"tatte",sp:true},{k:"そらを",r:"sora wo",sp:true},{k:"みあげました",r:"miage mashita",sp:false},{k:"。",r:""}
      ],
      [
        {k:"このうつくしい",r:"kono utsukushii",sp:true},{k:"はる",r:"haru",sp:true},{k:"は",r:"wa",sp:true},{k:"ながく",r:"nagaku",sp:true},{k:"つづかない",r:"tsudzukanai",sp:true},{k:"でしょう",r:"deshou",sp:false},{k:"。",r:""}
      ],
      [
        {k:"だからこそ",r:"dakara koso",sp:true},{k:"このしゅんかんを",r:"kono shunkan wo",sp:true},{k:"ずっと",r:"zutto",sp:true},{k:"おぼえていたい",r:"oboete itai",sp:true},{k:"です",r:"desu",sp:false},{k:"。",r:""}
      ],
    ]
  },
];

// ══════════════════════════════════════
// STATE
// ══════════════════════════════════════
const levels = ["Semua", "Mudah", "Sedang", "Sulit"];
let activeLevel = "Semua";
let activeStoryId = null;
let revealedWords = new Set();
let showAll = false;

// ══════════════════════════════════════
// INIT
// ══════════════════════════════════════
function init() {
  buildLevelTabs();
  buildStoryList();
}

function buildLevelTabs() {
  const wrap = document.getElementById('level-tabs');
  wrap.innerHTML = '';
  levels.forEach(l => {
    const btn = document.createElement('button');
    btn.className = 'level-btn' + (l === activeLevel ? ' active' : '');
    btn.textContent = l;
    btn.onclick = () => { activeLevel = l; buildLevelTabs(); buildStoryList(); };
    wrap.appendChild(btn);
  });
}

function buildStoryList() {
  const list = document.getElementById('story-list');
  const filtered = activeLevel === 'Semua' ? stories : stories.filter(s => s.level === activeLevel);
  list.innerHTML = '';
  filtered.forEach(s => {
    const card = document.createElement('div');
    card.className = 'story-card' + (s.id === activeStoryId ? ' active' : '');
    const levelClass = s.level === 'Mudah' ? 'easy' : s.level === 'Sedang' ? 'medium' : 'hard';
    card.innerHTML = `
      <div class="story-meta">
        <div class="story-title-jp">${s.titleJP}</div>
        <div class="story-title-id">${s.titleID}</div>
        <div class="story-tags">
          <span class="tag ${levelClass}">${s.level}</span>
          <span class="tag">${s.sentences.length} kalimat</span>
          <span class="tag">${countWords(s)} kata</span>
        </div>
      </div>
      <div class="story-arrow">›</div>
    `;
    card.onclick = () => openStory(s.id);
    list.appendChild(card);
  });
}

function countWords(s) {
  return s.sentences.reduce((acc, sent) => acc + sent.filter(w => w.r && w.k !== '。' && w.k !== '：' && !w.k.includes('「') && !w.k.includes('」')).length, 0);
}

// ══════════════════════════════════════
// OPEN STORY
// ══════════════════════════════════════
function openStory(id) {
  activeStoryId = id;
  revealedWords = new Set();
  showAll = false;
  buildStoryList();

  const story = stories.find(s => s.id === id);
  document.getElementById('pane-jp').textContent = story.titleJP;
  document.getElementById('pane-id').textContent = story.titleID;
  document.getElementById('meaning-text').textContent = story.translation;
  document.getElementById('btn-reveal-all').classList.remove('on');
  document.getElementById('btn-reveal-all').textContent = 'Tampilkan Semua';

  renderText(story);
  buildVocab(story);
  updateScore(story);

  const pane = document.getElementById('reading-pane');
  pane.classList.add('show');
  pane.scrollIntoView({ behavior: 'smooth', block: 'start' });

  // Nav buttons
  const ids = (activeLevel === 'Semua' ? stories : stories.filter(s => s.level === activeLevel)).map(s => s.id);
  const pos = ids.indexOf(id);
  document.getElementById('btn-prev').disabled = pos <= 0;
  document.getElementById('btn-next').disabled = pos >= ids.length - 1;
}

function renderText(story) {
  const body = document.getElementById('text-body');
  body.className = 'text-body' + (showAll ? ' show-all' : '');
  body.innerHTML = '';

  story.sentences.forEach((sent, si) => {
    sent.forEach((word, wi) => {
      if (!word.r && (word.k === '。' || word.k === '：')) {
        const punc = document.createElement('span');
        punc.textContent = word.k;
        body.appendChild(punc);
        return;
      }
      if (!word.r) return;

      const wordId = `${si}-${wi}`;
      const span = document.createElement('span');
      span.className = 'w' + (revealedWords.has(wordId) ? ' revealed' : '');
      span.dataset.id = wordId;
      span.onclick = () => revealWord(wordId, story);

      const furi = document.createElement('span');
      furi.className = 'furi';
      furi.textContent = word.r;

      span.appendChild(furi);
      span.appendChild(document.createTextNode(word.k));
      body.appendChild(span);

      if (word.sp) {
        body.appendChild(document.createTextNode('\u200b'));
      }
    });

    // Line break between sentences
    if (si < story.sentences.length - 1) {
      body.appendChild(document.createElement('br'));
    }
  });
}

function revealWord(id, story) {
  if (showAll) return;
  revealedWords.add(id);
  const el = document.querySelector(`.w[data-id="${id}"]`);
  if (el) el.classList.add('revealed');
  updateScore(story);
}

function updateScore(story) {
  const total = countWords(story);
  const revealed = revealedWords.size;
  document.getElementById('score-revealed').textContent = revealed;
  document.getElementById('score-total').textContent = total;
  const pct = total > 0 ? (revealed / total) * 100 : 0;
  document.getElementById('score-fill').style.width = pct + '%';
}

function toggleRevealAll() {
  showAll = !showAll;
  const btn = document.getElementById('btn-reveal-all');
  btn.classList.toggle('on', showAll);
  btn.textContent = showAll ? 'Sembunyikan' : 'Tampilkan Semua';
  const story = stories.find(s => s.id === activeStoryId);
  renderText(story);
}

function resetReveals() {
  revealedWords = new Set();
  showAll = false;
  document.getElementById('btn-reveal-all').classList.remove('on');
  document.getElementById('btn-reveal-all').textContent = 'Tampilkan Semua';
  const story = stories.find(s => s.id === activeStoryId);
  renderText(story);
  updateScore(story);
}

function buildVocab(story) {
  const grid = document.getElementById('vocab-grid');
  grid.innerHTML = '';
  story.vocab.forEach(v => {
    grid.innerHTML += `
      <div class="vocab-item">
        <span class="vocab-kana">${v.kana}</span>
        <div class="vocab-roma">${v.romaji}</div>
        <div class="vocab-mean">${v.mean}</div>
      </div>
    `;
  });
}

function navStory(dir) {
  const ids = (activeLevel === 'Semua' ? stories : stories.filter(s => s.level === activeLevel)).map(s => s.id);
  const pos = ids.indexOf(activeStoryId);
  const newPos = pos + dir;
  if (newPos >= 0 && newPos < ids.length) openStory(ids[newPos]);
}

init();
</script>
</body>
</html>
