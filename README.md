# weike<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>微分的定义 - 试讲PPT</title>
    <script src="https://polyfill.io/v3/polyfill.min.js?features=es6"></script>
    <script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>
    <style>
        body {
            font-family: "Microsoft YaHei", "Segoe UI", sans-serif;
            background-color: #f0f2f5;
            margin: 0;
            padding: 20px;
            display: flex;
            flex-direction: column;
            align-items: center;
        }
        .slide-container {
            width: 960px; /* 16:9 ratio */
            height: 540px;
            background: white;
            margin-bottom: 40px;
            box-shadow: 0 4px 15px rgba(0,0,0,0.1);
            position: relative;
            overflow: hidden;
            padding: 40px;
            box-sizing: border-box;
            display: flex;
            flex-direction: column;
        }
        .slide-number {
            position: absolute;
            bottom: 20px;
            right: 20px;
            color: #ccc;
            font-size: 14px;
        }
        h1 { color: #2c3e50; margin-bottom: 10px; }
        h2 { color: #34495e; font-size: 28px; border-bottom: 2px solid #3498db; padding-bottom: 10px; margin-top: 0; }
        h3 { color: #2980b9; margin-top: 20px; }
        p, li { font-size: 20px; line-height: 1.6; color: #555; }
        .highlight { color: #e74c3c; font-weight: bold; }
        .blue-box {
            background-color: #eaf2f8;
            border-left: 5px solid #3498db;
            padding: 15px;
            margin: 15px 0;
        }
        .center-content {
            flex: 1;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            text-align: center;
        }
        .columns {
            display: flex;
            flex: 1;
        }
        .col-half {
            width: 50%;
            padding: 10px;
        }
        .placeholder-img {
            width: 100%;
            height: 250px;
            background-color: #eee;
            border: 2px dashed #aaa;
            display: flex;
            justify-content: center;
            align-items: center;
            color: #777;
            font-style: italic;
        }
        table { width: 100%; border-collapse: collapse; margin-top: 20px; }
        th, td { border: 1px solid #ddd; padding: 12px; text-align: left; font-size: 20px; }
        th { background-color: #f8f9fa; color: #2c3e50; }
    </style>
</head>
<body>

    <div class="slide-container">
        <div class="center-content">
            <h1 style="font-size: 56px; margin-bottom: 20px;">微分的定义</h1>
            <p style="font-size: 28px; color: #7f8c8d;">——从“以直代曲”的线性近似谈起</p>
            <div style="margin-top: 60px; font-size: 24px;">
                <p><strong>试讲人：张金涛</strong></p>
                <p>202X年X月X日</p>
            </div>
        </div>
        <div class="slide-number">1 / 10</div>
    </div>

    <div class="slide-container">
        <h2>目录 / Contents</h2>
        <div class="center-content" style="align-items: flex-start; padding-left: 100px;">
            <ul style="font-size: 28px; list-style-type: none;">
                <li style="margin-bottom: 30px;"><strong>01</strong> 微分的定义 <span style="color:#999; font-size: 20px;">(Definition)</span></li>
                <li style="margin-bottom: 30px;"><strong>02</strong> 微分与导数的关系 <span style="color:#999; font-size: 20px;">(Relationship)</span></li>
                <li style="margin-bottom: 30px;"><strong>03</strong> 一阶微分的形式不变性 <span style="color:#999; font-size: 20px;">(Invariance)</span></li>
                <li><strong>04</strong> 微分的用途 <span style="color:#999; font-size: 20px;">(Application)</span></li>
            </ul>
        </div>
        <div class="slide-number">2 / 10</div>
    </div>

    <div class="slide-container">
        <h2>01 引例：复杂的非线性增量</h2>
        <div class="columns">
            <div class="col-half">
                <div class="placeholder-img">
                    此处插入：函数曲线图<br>
                    标注点 M(x₀, y₀) 和 N(x₀+Δx, y₀+Δy)<br>
                    展示曲线上的真实增量 Δy
                </div>
            </div>
            <div class="col-half" style="padding-top: 20px;">
                <p><strong>问题提出：</strong></p>
                <p>当自变量产发生微小变化 $\Delta x$ 时，函数 $y=f(x)$ 的改变量 $\Delta y$ 往往是非线性的，计算非常复杂。</p>
                <p class="blue-box">
                    <strong>思考：</strong><br>
                    能否找到一个关于 $\Delta x$ 的<strong>线性函数</strong>（即一次函数），来近似替代复杂的 $\Delta y$？
                </p>
            </div>
        </div>
        <div class="slide-number">3 / 10</div>
    </div>

    <div class="slide-container">
        <h2>01 微分的定义</h2>
        <div style="padding: 0 20px;">
            <p><strong>定义 4.3.1</strong></p>
            <p>设函数 $y=f(x)$ 在 $U(x_0, \delta)$ 内有定义。如果增量 $\Delta y$ 可以表示为：</p>
            <div style="text-align: center; font-size: 28px; margin: 20px 0;">
                $$ \Delta y = A\Delta x + o(\Delta x) \quad (\Delta x \to 0) $$
            </div>
            <p>其中 $A$ 为常数，则称 $f(x)$ 在点 $x_0$ 处<strong>可微</strong>。</p>
            <div class="blue-box">
                <ul>
                    <li>$A\Delta x$ 称为 $f(x)$ 在点 $x_0$ 处的<strong>微分</strong>，记作 <span class="highlight">$dy$</span> 或 $df(x_0)$。</li>
                    <li>$dy = A\Delta x$ 是 $\Delta y$ 的<strong>线性主部</strong>。</li>
                </ul>
            </div>
        </div>
        <div class="slide-number">4 / 10</div>
    </div>

    <div class="slide-container">
        <h2>01 微分的几何意义</h2>
        <div class="columns">
            <div class="col-half">
                <div class="placeholder-img">
                    此处插入：微分几何意义图<br>
                    重点区分 Δy (曲线增量)<br>
                    和 dy (切线增量)
                </div>
            </div>
            <div class="col-half">
                <h3>几何解释</h3>
                <ul>
                    <li><strong>$\Delta y$</strong>：曲线上的纵坐标增量（精确值）</li>
                    <li><strong>$dy$</strong>：切线上的纵坐标增量（近似值）</li>
                    <li><strong>$o(\Delta x)$</strong>：当 $\Delta x \to 0$ 时，切线与曲线的高阶无穷小误差</li>
                </ul>
                <p style="text-align: center; font-weight: bold; font-size: 24px; margin-top:30px;">
                    “以直代曲”<br>
                    $\Delta y \approx dy$
                </p>
            </div>
        </div>
        <div class="slide-number">5 / 10</div>
    </div>

    <div class="slide-container">
        <h2>02 微分公式与微商</h2>
        <p>对于自变量 $x$，我们规定其微分等于其增量，即 <span class="highlight">$dx = \Delta x$</span>。</p>
        <p>因此，函数 $y=f(x)$ 的微分公式可写为：</p>
        <div style="text-align: center; font-size: 32px; margin: 30px 0; color: #2980b9;">
            $$ dy = f'(x)dx $$
        </div>
        <p>由此可见：</p>
        <div style="text-align: center; font-size: 24px;">
            $$ \frac{dy}{dx} = f'(x) $$
        </div>
        <p style="text-align: center; color: #7f8c8d;">这也是导数被称为“微商”（微分之商）的原因。</p>
        <div class="slide-number">6 / 10</div>
    </div>

    <div class="slide-container">
        <h2>02 微分与导数的关系</h2>
        <div class="blue-box">
            <p><strong>定理 4.3.1 (可微与可导的关系)</strong></p>
            <p>函数 $f(x)$ 在点 $x_0$ 处可微的充分必要条件是 $f(x)$ 在点 $x_0$ 处可导。</p>
        </div>
        <p>且系数 $A$ 恰好等于导数值：</p>
        <div style="text-align: center; font-size: 28px;">
            $$ A = f'(x_0) $$
        </div>
        <p style="margin-top: 40px; font-style: italic;">(注：必要性与充分性的证明过程将在黑板演示)</p>
        <div class="slide-number">7 / 10</div>
    </div>

    <div class="slide-container">
        <h2>03 一阶微分形式不变性</h2>
        <p>设 $y = f(u)$，考察以下两种情况：</p>
        <table>
            <tr>
                <th width="50%">情形 1：$u$ 是自变量</th>
                <th width="50%">情形 2：$u = g(x)$ 是中间变量</th>
            </tr>
            <tr>
                <td>$$ dy = f'(u)du $$</td>
                <td>$$ dy = f'(u)g'(x)dx $$<br>因 $du = g'(x)dx$，故：<br>$$ dy = f'(u)du $$</td>
            </tr>
        </table>
        <div class="blue-box" style="margin-top: 30px;">
            <strong>结论：</strong>
            无论 $u$ 是自变量还是中间变量，微分形式 $dy = f'(u)du$ 保持不变。
        </div>
        <div class="slide-number">8 / 10</div>
    </div>

    <div class="slide-container">
        <h2>04 微分的用途：近似计算</h2>
        <p><strong>例题：求 $\sqrt[4]{80}$ 的近似值。</strong></p>
        <div class="columns">
            <div class="col-half">
                <p><strong>1. 构造函数与选点：</strong></p>
                <p>设 $f(x) = x^{\frac{1}{4}}$</p>
                <p>取 $x_0 = 81$ (因 $81^{\frac{1}{4}}=3$ 易算)</p>
                <p>则 $\Delta x = 80 - 81 = -1$</p>
            </div>
            <div class="col-half">
                <p><strong>2. 利用公式计算：</strong></p>
                <p>$$ f(x_0+\Delta x) \approx f(x_0) + f'(x_0)\Delta x $$</p>
                <p>$$ f'(x) = \frac{1}{4}x^{-\frac{3}{4}} \Rightarrow f'(81) = \frac{1}{108} $$</p>
                <p>$$ \sqrt[4]{80} \approx 3 + \frac{1}{108} \times (-1) \approx 2.9907 $$</p>
            </div>
        </div>
        <div class="slide-number">9 / 10</div>
    </div>

    <div class="slide-container">
        <div class="center-content">
            <h1 style="color: #2980b9;">谢 谢 观 看</h1>
            <p style="font-size: 24px; margin-top: 20px;">请各位评委老师批评指正</p>
            <hr style="width: 100px; border: 2px solid #3498db; margin: 40px auto;">
            <p>试讲人：张金涛</p>
        </div>
        <div class="slide-number">10 / 10</div>
    </div>

</body>
</html>