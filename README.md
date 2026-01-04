from pathlib import Path, PurePosixPath

html = r"""<!doctype html>
<html lang="zh-CN">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>微分的定义｜15分钟试讲</title>
  <style>
    :root{
      --bg:#ffffff;
      --fg:#111;
      --muted:#555;
      --accent:#1f4ed8;
      --card:#f5f7fb;
      --border:#e6e8ef;
      --shadow: 0 10px 30px rgba(0,0,0,.08);
      --font: ui-sans-serif, system-ui, -apple-system, "PingFang SC","Microsoft YaHei","Noto Sans CJK SC", Arial, sans-serif;
    }
    html,body{height:100%; margin:0; background:var(--bg); color:var(--fg); font-family:var(--font);}
    .deck{height:100%; width:100%; overflow:hidden; position:relative;}
    .slide{
      height:100%; width:100%;
      box-sizing:border-box;
      padding:56px 72px;
      display:none;
      position:absolute; inset:0;
      background:var(--bg);
    }
    .slide.active{display:block;}
    .topbar{
      display:flex; align-items:flex-end; justify-content:space-between;
      margin-bottom:26px;
    }
    .kicker{
      font-size:18px; color:var(--muted);
      letter-spacing:.08em;
    }
    .kicker b{color:var(--accent); font-weight:700;}
    .meta{
      font-size:16px; color:var(--muted);
    }
    h1{margin:0; font-size:56px; line-height:1.1;}
    h2{margin:0; font-size:44px; line-height:1.12;}
    .subtitle{margin-top:12px; font-size:22px; color:var(--muted);}
    .content{
      margin-top:28px;
      font-size:28px; line-height:1.45;
      max-width:1100px;
    }
    .content ul{margin:0; padding-left:1.25em;}
    .content li{margin:10px 0;}
    .callout{
      margin-top:20px;
      padding:18px 22px;
      background:var(--card);
      border:1px solid var(--border);
      border-radius:16px;
      box-shadow:var(--shadow);
      font-size:26px;
    }
    .two-col{
      display:grid;
      grid-template-columns: 1.15fr .85fr;
      gap:28px;
      align-items:start;
    }
    .box{
      padding:18px 22px;
      border:1px solid var(--border);
      border-radius:16px;
      background:#fff;
    }
    .box h3{
      margin:0 0 10px 0;
      font-size:22px;
      color:var(--accent);
      letter-spacing:.02em;
    }
    .formula{
      font-size:30px;
      margin-top:14px;
    }
    .tiny{font-size:18px; color:var(--muted); margin-top:14px;}
    .progress{
      position:absolute; left:0; bottom:0;
      height:6px; width:100%;
      background:var(--border);
    }
    .progress > div{
      height:100%; width:0%;
      background:var(--accent);
      transition:width .25s ease;
    }
    .navhint{
      position:absolute; right:18px; bottom:14px;
      font-size:14px; color:var(--muted);
      user-select:none;
    }
    .notes{
      position:absolute;
      left:72px; right:72px; bottom:26px;
      background:#fff7e6;
      border:1px solid #f3d29b;
      color:#6a3b00;
      border-radius:16px;
      padding:14px 18px;
      box-shadow:var(--shadow);
      display:none;
      font-size:18px;
      line-height:1.4;
    }
    .notes.show{display:block;}
    .notes b{color:#7a4200;}
    .divider{
      height:1px; background:var(--border);
      margin:18px 0;
    }
    .badge{
      display:inline-block;
      padding:6px 10px;
      border-radius:999px;
      background:rgba(31,78,216,.08);
      color:var(--accent);
      font-size:16px;
      border:1px solid rgba(31,78,216,.18);
      margin-right:10px;
      vertical-align:middle;
    }
    .big-number{
      font-size:96px;
      font-weight:800;
      color:rgba(31,78,216,.12);
      line-height:1;
      margin:0;
    }
    .center{
      display:flex;
      height:calc(100% - 90px);
      align-items:center;
    }
    .center > div{max-width:1100px;}
    /* MathJax sizing */
    mjx-container[jax="CHTML"]{font-size: 112%;}
    /* Print (optional) */
    @media print{
      .slide{display:block; position:relative; page-break-after:always; height:100vh;}
      .progress,.navhint,.notes{display:none !important;}
    }
  </style>
  <!-- MathJax (requires internet). If offline, formulas will still show as plain text in the HTML. -->
  <script>
    window.MathJax = { tex: { inlineMath: [['$','$'], ['\\(','\\)']] } };
  </script>
  <script defer src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>
</head>

<body>
<div class="deck" id="deck">

  <!-- 1 -->
  <section class="slide active" data-title="微分的定义">
    <div class="topbar">
      <div class="kicker"><b>高等数学</b>｜微分</div>
      <div class="meta">试讲时间：15分钟</div>
    </div>
    <h1>微分的定义</h1>
    <div class="subtitle">从“增量”到“线性主部”</div>
    <div class="content">
      <div class="callout">
        今天目标：让学生在 15 分钟内回答两句话：<br/>
        ① 什么是微分（$dy$ 的含义是什么）？<br/>
        ② 为什么 $dy=f'(x)\,dx$ 能用来近似与求导？
      </div>
    </div>
    <div class="notes">
      <b>讲解提示：</b>开场先定目标，强调“微分=线性近似的主部”。提问：为什么我们总写 $dy$ 而不是 $\Delta y$？
    </div>
  </section>

  <!-- 2 -->
  <section class="slide" data-title="提纲">
    <div class="topbar">
      <div class="kicker"><b>提纲</b></div>
      <div class="meta">按“概念 → 关系 → 性质 → 应用”</div>
    </div>
    <h2>这节课讲四件事</h2>
    <div class="content">
      <ul>
        <li><span class="badge">01</span>微分的定义：增量的线性主部</li>
        <li><span class="badge">02</span>微分与导数：$A=f'(x_0)$</li>
        <li><span class="badge">03</span>形式不变性：换变量仍保持 $dy=f'(x)dx$</li>
        <li><span class="badge">04</span>用途：快速求导、近似估计与误差</li>
      </ul>
      <div class="tiny">操作：←/→ 翻页，按 N 显示/隐藏讲稿提示</div>
    </div>
    <div class="notes">
      <b>讲解提示：</b>告诉学生：每一部分都配一个“马上能用”的例子，增强获得感。
    </div>
  </section>

  <!-- 3 -->
  <section class="slide" data-title="01 微分的直观">
    <div class="topbar">
      <div class="kicker"><b>01</b> 微分的定义</div>
      <div class="meta">关键词：线性近似</div>
    </div>
    <h2>先看“增量”怎么分解</h2>
    <div class="content two-col">
      <div>
        <ul>
          <li>自变量从 $x_0$ 变到 $x_0+\Delta x$，函数增量：$\Delta y=f(x_0+\Delta x)-f(x_0)$</li>
          <li>核心思想：当 $\Delta x$ 很小时，$\Delta y$ 可以拆成：</li>
        </ul>
        <div class="callout formula">
          $\displaystyle \Delta y=\underbrace{A\Delta x}_{\text{线性主部}}+\underbrace{o(\Delta x)}_{\text{高阶小量}}$
        </div>
        <div class="tiny">其中 $o(\Delta x)$ 表示比 $\Delta x$ 小得更快的量：$\lim\limits_{\Delta x\to 0}\frac{o(\Delta x)}{\Delta x}=0$</div>
      </div>
      <div class="box">
        <h3>一句话解释</h3>
        <div style="font-size:24px; line-height:1.5;">
          <p style="margin:0;">把“弯曲”的变化</p>
          <p style="margin:0;">拆成“直线的变化 + 很小的弯曲误差”。</p>
          <div class="divider"></div>
          <p style="margin:0;">微分，就是这条“直线变化”的量。</p>
        </div>
      </div>
    </div>
    <div class="notes">
      <b>讲解提示：</b>用“切线近似曲线”解释线性主部。强调：微分不是增量本身，而是增量的主部（可加、可线性运算）。
    </div>
  </section>

  <!-- 4 -->
  <section class="slide" data-title="01 微分的形式定义">
    <div class="topbar">
      <div class="kicker"><b>01</b> 微分的定义</div>
      <div class="meta">严格表述</div>
    </div>
    <h2>定义：可微 ⇔ 存在微分</h2>
    <div class="content">
      <div class="callout">
        若存在常数 $A$，使得当 $\Delta x\to 0$ 时
        <div class="formula">$\displaystyle \Delta y=f(x_0+\Delta x)-f(x_0)=A\Delta x+o(\Delta x)$</div>
        则称 $f(x)$ 在 $x_0$ <b>可微</b>，并把线性主部定义为<b>微分</b>：
        <div class="formula">$\displaystyle dy = A\,dx\quad (\text{其中 } dx=\Delta x)$</div>
      </div>

      <ul style="margin-top:18px;">
        <li><b>dx</b>：人为规定的自变量“微小改变量”（取 $dx=\Delta x$）</li>
        <li><b>dy</b>：对应的线性主部（切线给出的变化）</li>
      </ul>
    </div>
    <div class="notes">
      <b>讲解提示：</b>提醒学生：这里的 $dx$ 不是“无限小的神秘量”，而是把 $\Delta x$ 直接改名成 $dx$，方便表达“主部”。
    </div>
  </section>

  <!-- 5 -->
  <section class="slide" data-title="01 一个秒懂例子">
    <div class="topbar">
      <div class="kicker"><b>01</b> 微分的定义</div>
      <div class="meta">例：$f(x)=x^2$</div>
    </div>
    <h2>例：$f(x)=x^2$ 在 $x_0$ 处的微分</h2>
    <div class="content">
      <div class="callout formula">
        $\Delta y=(x_0+\Delta x)^2-x_0^2=2x_0\Delta x+(\Delta x)^2$
      </div>
      <ul>
        <li>线性主部：$A\Delta x=2x_0\Delta x$，高阶小量：$o(\Delta x)=(\Delta x)^2$</li>
        <li>因此 $A=2x_0$，微分为：$\displaystyle dy = 2x_0\,dx$</li>
        <li>理解：在 $x_0$ 处，曲线用切线近似，斜率是 $2x_0$</li>
      </ul>
    </div>
    <div class="notes">
      <b>讲解提示：</b>顺手问：为什么 $(\Delta x)^2$ 是 $o(\Delta x)$？让学生说出极限比值为 0。
    </div>
  </section>

  <!-- 6 -->
  <section class="slide" data-title="02 微分与导数">
    <div class="topbar">
      <div class="kicker"><b>02</b> 微分与导数的关系</div>
      <div class="meta">导数是“主部系数”</div>
    </div>
    <h2>同一个 $A$，两个名字</h2>
    <div class="content">
      <ul>
        <li>由定义：$\Delta y=A\Delta x+o(\Delta x)$</li>
        <li>两边除以 $\Delta x$（$\Delta x\neq 0$）：</li>
      </ul>
      <div class="callout formula">
        $\displaystyle \frac{\Delta y}{\Delta x}=A+\frac{o(\Delta x)}{\Delta x}\ \xrightarrow[\Delta x\to 0]{}\ A$
      </div>
      <ul>
        <li>因此 $\displaystyle f'(x_0)=\lim_{\Delta x\to 0}\frac{\Delta y}{\Delta x}=A$</li>
        <li>结论：<b>可微 ⇒ 可导</b>，并且</li>
      </ul>
      <div class="callout formula">
        $\displaystyle dy = f'(x_0)\,dx$
      </div>
    </div>
    <div class="notes">
      <b>讲解提示：</b>强调：导数是微分中“乘在 dx 前面的系数”。如果学生熟导数，从导数回到微分就很自然。
    </div>
  </section>

  <!-- 7 -->
  <section class="slide" data-title="02 一个应用小例">
    <div class="topbar">
      <div class="kicker"><b>02</b> 微分与导数的关系</div>
      <div class="meta">例：切线近似</div>
    </div>
    <h2>用微分表达线性近似</h2>
    <div class="content">
      <div class="callout formula">
        $\displaystyle \Delta y = dy + o(\Delta x) = f'(x_0)\Delta x + o(\Delta x)$
      </div>
      <ul>
        <li>当 $\Delta x$ 很小时：$\Delta y \approx dy$</li>
        <li>等价写法（线性化）：$\displaystyle f(x_0+\Delta x)\approx f(x_0)+f'(x_0)\Delta x$</li>
      </ul>

      <div class="two-col" style="margin-top:18px;">
        <div class="box">
          <h3>这句话的“物理含义”</h3>
          <div style="font-size:24px; line-height:1.5;">
            <p style="margin:0;">微分给出“最主要”的变化。</p>
            <p style="margin:0;">误差来自高阶项。</p>
          </div>
        </div>
        <div class="box">
          <h3>一句口播</h3>
          <div style="font-size:24px; line-height:1.5;">
            “函数在一点附近，看起来像它的切线。”
          </div>
        </div>
      </div>
    </div>
    <div class="notes">
      <b>讲解提示：</b>把“线性化”当成后面近似估计的伏笔。此页不要展开太久（约 1 分钟）。
    </div>
  </section>

  <!-- 8 -->
  <section class="slide" data-title="03 形式不变性">
    <div class="topbar">
      <div class="kicker"><b>03</b> 一阶微分的形式不变性</div>
      <div class="meta">换元仍成立</div>
    </div>
    <h2>形式不变性：像“链式法则”一样好用</h2>
    <div class="content">
      <ul>
        <li>一元函数：$\displaystyle y=f(x)\Rightarrow dy=f'(x)\,dx$</li>
        <li>若 $x=\varphi(t)$，则 $y=f(\varphi(t))$，有：</li>
      </ul>
      <div class="callout formula">
        $\displaystyle dy = f'(x)\,dx = f'(\varphi(t))\cdot \varphi'(t)\,dt$
      </div>
      <ul>
        <li>注意：表达式的<b>形式</b>没有变（仍是 “导数 × 微小改变量”）</li>
        <li>本质：一阶微分是线性的，符合“复合函数的线性近似”</li>
      </ul>
    </div>
    <div class="notes">
      <b>讲解提示：</b>点到为止：告诉学生“这就是链式法则的微分写法”。不要做太多证明。
    </div>
  </section>

  <!-- 9 -->
  <section class="slide" data-title="03 一页证明思路">
    <div class="topbar">
      <div class="kicker"><b>03</b> 一阶微分的形式不变性</div>
      <div class="meta">证明（讲思路）</div>
    </div>
    <h2>证明思路：抓住“线性主部”</h2>
    <div class="content">
      <ul>
        <li>先写 $x=\varphi(t)$ 的增量：$\Delta x = \varphi(t+\Delta t)-\varphi(t)$</li>
        <li>若 $\varphi$ 在 $t$ 处可导：$\Delta x = \varphi'(t)\Delta t + o(\Delta t)$</li>
        <li>把它代入 $y=f(x)$ 的微分展开：</li>
      </ul>
      <div class="callout formula">
        $\displaystyle \Delta y = f'(x)\Delta x + o(\Delta x)
        \approx f'(\varphi(t))\cdot \varphi'(t)\,\Delta t$
      </div>
      <div class="tiny">一句话：复合函数的“主部”=主部套主部。</div>
    </div>
    <div class="notes">
      <b>讲解提示：</b>把证明压缩成 3 句：写 Δx、再写 Δy、最后代入比较主部。学生能跟住即可。
    </div>
  </section>

  <!-- 10 -->
  <section class="slide" data-title="04 微分的用途">
    <div class="topbar">
      <div class="kicker"><b>04</b> 微分的用途</div>
      <div class="meta">两类：求导 & 近似</div>
    </div>
    <h2>微分为什么重要？</h2>
    <div class="content two-col">
      <div class="box">
        <h3>用途 A：快速求导（尤其是复合函数）</h3>
        <div style="font-size:26px; line-height:1.5;">
          用“微分规则”直接写 $dy$，再读出 $y'$。
        </div>
      </div>
      <div class="box">
        <h3>用途 B：近似估计（线性化）</h3>
        <div style="font-size:26px; line-height:1.5;">
          用 $f(x_0+\Delta x)\approx f(x_0)+f'(x_0)\Delta x$ 做心算。
        </div>
      </div>
      <div style="grid-column:1/-1" class="callout">
        记住一句话：<b>微分 = 线性近似工具</b>（既能推公式，也能算数值）。
      </div>
    </div>
    <div class="notes">
      <b>讲解提示：</b>这一页是“转场页”，不要停留太久。直接进入两个例子。
    </div>
  </section>

  <!-- 11 -->
  <section class="slide" data-title="04 用途：快速求导">
    <div class="topbar">
      <div class="kicker"><b>04</b> 微分的用途</div>
      <div class="meta">例：$y=\sin(x^2)$</div>
    </div>
    <h2>用途 A：用微分快速求导</h2>
    <div class="content">
      <div class="callout formula">
        $y=\sin(x^2)\quad\Rightarrow\quad dy=\cos(x^2)\,d(x^2)=\cos(x^2)\cdot 2x\,dx$
      </div>
      <ul>
        <li>因此 $\displaystyle y'=\frac{dy}{dx}=2x\cos(x^2)$</li>
        <li>优势：不必“背”链式法则的层层写法，直接按微分规则拆开。</li>
      </ul>
      <div class="tiny">课堂口播建议：先写 $dy$，再“除以 $dx$”。</div>
    </div>
    <div class="notes">
      <b>讲解提示：</b>强调“d( ) 里面当成整体”。这页让听课老师看到你的板书节奏：一行 $dy$，一行 $y'$。
    </div>
  </section>

  <!-- 12 -->
  <section class="slide" data-title="04 用途：近似估计">
    <div class="topbar">
      <div class="kicker"><b>04</b> 微分的用途</div>
      <div class="meta">例：$\sqrt{4.1}$</div>
    </div>
    <h2>用途 B：用微分做近似估计</h2>
    <div class="content">
      <ul>
        <li>令 $f(x)=\sqrt{x}$，取 $x_0=4$，则 $f(4)=2$</li>
        <li>$f'(x)=\dfrac{1}{2\sqrt{x}}$，所以 $f'(4)=\dfrac14$</li>
        <li>$\Delta x=0.1$，线性近似：</li>
      </ul>
      <div class="callout formula">
        $\displaystyle \sqrt{4.1}=f(4+0.1)\approx f(4)+f'(4)\cdot 0.1
        =2+\frac14\cdot 0.1=2.025$
      </div>
      <div class="tiny">解释误差：忽略的是高阶项（大约与 $(\Delta x)^2$ 同阶）。</div>
    </div>
    <div class="notes">
      <b>讲解提示：</b>这是展示“微分能算数”的亮点例子。最后补一句：实际值约 2.0249…（不必追求精确）。
    </div>
  </section>

  <!-- 13 -->
  <section class="slide" data-title="总结与结束">
    <div class="topbar">
      <div class="kicker"><b>总结</b></div>
      <div class="meta">谢谢</div>
    </div>
    <h2>三句话带走</h2>
    <div class="content">
      <ul>
        <li>微分：把增量 $\Delta y$ 的<b>线性主部</b>抽出来，记作 $dy$。</li>
        <li>导数：微分中乘在 $dx$ 前的系数，$dy=f'(x)\,dx$。</li>
        <li>应用：$dy$ 既能快速求导，也能做线性近似与误差估计。</li>
      </ul>
      <div class="callout" style="margin-top:18px;">
        <b>结束语：</b>“把复杂变化先线性化，这是微积分最实用的思想之一。”
      </div>
      <div class="navhint" style="right:72px; bottom:22px; font-size:16px;">
        结束｜谢谢！
      </div>
    </div>
    <div class="notes">
      <b>讲解提示：</b>收尾 20 秒：复述三点 + 结束语。若有追问，优先解释“可微与可导”的逻辑链。
    </div>
  </section>

  <div class="progress" aria-hidden="true"><div id="bar"></div></div>
  <div class="navhint" aria-hidden="true">←/→ 翻页 · N 显示讲稿</div>
</div>

<script>
(function(){
  const slides = Array.from(document.querySelectorAll('.slide'));
  let idx = 0;
  let notesOn = false;

  function render(){
    slides.forEach((s,i)=>s.classList.toggle('active', i===idx));
    const bar = document.getElementById('bar');
    bar.style.width = ((idx+1)/slides.length*100).toFixed(2) + '%';

    // Update hash for quick navigation
    const title = slides[idx].dataset.title || ('slide-' + (idx+1));
    history.replaceState(null, '', '#'+encodeURIComponent(String(idx+1)));

    // Notes
    slides.forEach(s=>{
      const n = s.querySelector('.notes');
      if(!n) return;
      n.classList.toggle('show', notesOn);
    });

    // Re-typeset MathJax on slide change (best-effort)
    if (window.MathJax && window.MathJax.typesetPromise) {
      window.MathJax.typesetPromise([slides[idx]]).catch(()=>{});
    }
  }

  function clamp(i){ return Math.max(0, Math.min(slides.length-1, i)); }

  function go(i){
    idx = clamp(i);
    render();
  }

  function next(){ go(idx+1); }
  function prev(){ go(idx-1); }

  // Keyboard
  window.addEventListener('keydown', (e)=>{
    const k = e.key;
    if(k === 'ArrowRight' || k === 'PageDown' || k === ' '){ e.preventDefault(); next(); }
    if(k === 'ArrowLeft' || k === 'PageUp'){ e.preventDefault(); prev(); }
    if(k === 'Home'){ e.preventDefault(); go(0); }
    if(k === 'End'){ e.preventDefault(); go(slides.length-1); }
    if(k === 'n' || k === 'N'){ notesOn = !notesOn; render(); }
  });

  // Hash navigation (#3)
  function fromHash(){
    const h = decodeURIComponent(location.hash.replace('#','')).trim();
    const n = parseInt(h,10);
    if(!Number.isNaN(n) && n>=1 && n<=slides.length) idx = n-1;
  }
  window.addEventListener('hashchange', ()=>{ fromHash(); render(); });

  fromHash();
  render();
})();
</script>
</body>
</html>
"""
out_path = Path("/mnt/data/微分的定义_15分钟试讲_简洁版.html")
out_path.write_text(html, encoding="utf-8")
str(out_path)

