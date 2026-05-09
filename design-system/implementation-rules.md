# implementation-rules.md
# 実装制約

## 基本方針

このLPは、後からHTML / CSS / Tailwind / React / Framer Motionで再現しやすい構造にする。
画像生成時の見た目をそのまま追うのではなく、実装では「カード」「グリッド」「セクション」「装飾パーツ」に分解して再現する。

## Recommended Section Structure

```html
<section class="section section--features">
  <div class="section__inner">
    <div class="section__heading"></div>
    <div class="section__body"></div>
  </div>
</section>
```

## Naming Direction

BEMまたはFLOCSS寄りで統一する。

例：

```txt
.l-section
.l-inner
.c-button
.c-ribbon
.c-divider
.c-card
.c-check-list
.p-hero
.p-features
.p-curriculum
.p-price
.p-final-cta
```

## Spacing Rules

### Section Padding

- PC: `96px〜140px`
- Tablet: `80px〜112px`
- SP: `64px〜88px`

### Inner Width

- max-width: `1080px〜1200px`
- padding-inline: `20px〜32px`

### Card Padding

- PC: `40px〜56px`
- SP: `24px〜32px`

## Responsive Rules

- PC 2カラム → SP 1カラム
- 3カラムカード → SP 1カラム or 2カラム
- 装飾の絶対配置はSPで非表示または縮小
- 大きな背景文字はSPでopacityを下げる
- 写真は `aspect-ratio` で管理する

## Image Rules

- `object-fit: cover`
- `aspect-ratio` を指定する
- 写真はカード内に収める
- 不規則な切り抜きは禁止
- 画像の上に長文テキストを重ねない

## Animation Rules

Framer Motionを使う場合は、控えめな演出に限定する。

使用可能：

- fade up
- slight slide
- opacity reveal
- stagger cards
- arrow subtle loop

禁止：

- 激しいパララックス
- 大きな回転
- 3D演出
- スクロールに依存しすぎる複雑な演出

## Componentization

推奨コンポーネント：

- `SectionHeading`
- `RibbonLabel`
- `DividerLine`
- `FeatureCard`
- `TimelineItem`
- `CheckList`
- `PriceCard`
- `LineButton`
- `GalleryGrid`
- `HandwrittenNote`

## CSS Decoration Implementation

### Marker Highlight

```css
.marker {
  background: linear-gradient(transparent 60%, rgba(181, 154, 106, 0.25) 60%);
}
```

### Faded Number

```css
.faded-number {
  position: absolute;
  font-family: serif;
  font-size: clamp(72px, 12vw, 160px);
  color: rgba(30, 30, 28, 0.05);
  line-height: 1;
  pointer-events: none;
}
```

### Thin Divider

```css
.divider {
  width: 100%;
  height: 1px;
  background: rgba(181, 154, 106, 0.35);
}
```

## Accessibility Rules

- CTAボタンは十分なコントラストを確保する
- 写真には具体的なaltを入れる
- 装飾画像は `aria-hidden="true"`
- 見出し階層を崩さない
- 文字サイズはSPでも14px未満にしない

## Avoid

- 実装困難な自由配置
- 画像生成特有の文字崩れをそのまま採用すること
- 装飾過多で本文が読めない状態
- すべてのセクションを黒背景にすること
- 写真に頼りすぎてUI構造が弱くなること
