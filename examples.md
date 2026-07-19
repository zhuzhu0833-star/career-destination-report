# Example snippets for filling report-visual.html

## STATS_HTML

```html
    <div class="stat">
      <div class="stat-num">+6%<small> /10年</small></div>
      <div class="stat-label">示例指标</div>
      <div class="stat-note">来源与口径说明</div>
    </div>
```

## PATHS_HTML

```html
    <div class="path-item">
      <div class="path-idx">01</div>
      <div>
        <h3>品牌管理</h3>
        <p>Brand Manager · 定位与跨部门经营</p>
        <span class="path-tag">快消 · 美妆</span>
      </div>
    </div>
```

## LADDERS_HTML

```html
    <div class="ladder-col" style="--accent:#0d7a78">
      <h3>快消品牌线</h3>
      <ol>
        <li>助理品牌经理</li>
        <li>品牌经理</li>
        <li>高级品牌经理</li>
        <li>品类总监</li>
      </ol>
    </div>
```

## TABS_HTML + PANELS_HTML

```html
    <button class="tab active" data-tab="r0" type="button">北美</button>
    <button class="tab" data-tab="r1" type="button">中国大陆</button>
```

```html
  <div class="panel active" id="panel-r0">
    <div class="employer-group">
      <h3><span class="dot"></span>科技</h3>
      <div class="employer-list">
        <div class="employer">
          <div><strong>Amazon</strong><span>Brand · Growth</span></div>
          <div class="badge">高频</div>
        </div>
      </div>
    </div>
  </div>
```

## SKILLS_HTML

```html
    <div class="skill-col" style="--accent:#0d7a78">
      <h3>硬技能</h3>
      <ul>
        <li>Excel / SQL</li>
      </ul>
    </div>
```

## COMPARE_SECTION（≥2 地区时）

复制模板中 section 结构，或使用：

```html
<section id="compare" class="reveal">
  <div class="section-label">05 · Compare</div>
  <h2 class="section-title">地区对比</h2>
  <p class="section-lead">热门赛道与入门通道差异。</p>
  <div class="compare">
    <div class="compare-head">维度</div>
    <div class="compare-head na">地区A</div>
    <div class="compare-head cn">地区B</div>
    <div class="compare-cell dim">热门赛道</div>
    <div class="compare-cell">...</div>
    <div class="compare-cell">...</div>
  </div>
</section>
```

单地区时将 `{{COMPARE_SECTION}}` 替换为空字符串。
