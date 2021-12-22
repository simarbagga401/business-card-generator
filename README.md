![image](https://user-images.githubusercontent.com/67456870/147143644-b734cbd8-0eef-4f0f-a058-bf104c2e8ab9.png)

## Live Demo
- See Live Demo of this project on https://generate-business-card.netlify.com

# Guide
## Dependencies
- Embed latest **html2canvas cdn** in your project's root *index.html* file.
- Run ```yarn install``` to install **yoyoo-ddr-vue3** (dependency to make elements moveable) & **@simonwep/pickr** (color picker dependency)

## *BusinessCard* Component
- This component provides a wrapper and acts as a **Card**
- Takes **Image** as prop to set Background Image of Card.
- Access  *changeBorderWidth(width), changeBorderColor(color), changeBorderRadius(value), printCard* Methods while using this component by providing *ref*.
```vue
  <BusinessCard
    ref="businessCard"
    :image="backgroundImage"
  >
```
```js
// Access businessCard Like This
     this.$refs.businessCard.printCard(imageFormat);
     this.$refs.businessCard.changeBorderColor(color);
```
## *DDR* Component
- View Docs for this vue library [yoyoo-ddr-vue3](https://github.com/zuimeiaj/yoyoo-ddr)
- DDR Component is a wrapper which makes elements Movable.
```vue
 <DDR
      :value="headingProperties"
      :parent="true"
      :active="cardHeadingActive"
    >
      <h1 id="cardHeading">HORIZEN</h1>
    </DDR>
```
```js
// Properties determining h1 tag's x,y offsets, width etc.
      headingProperties: {
        x: 230,
        y: 60,
        width: 200,
        height: 50,
        rotation: 0,
      },
// Determines if cardHeading is Active
      cardHeadingActive: true,
```

# Vue 3 + Vite

This template should help get you started developing with Vue 3 in Vite. The template uses Vue 3 `<script setup>` SFCs, check out the [script setup docs](https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup) to learn more.

## Recommended IDE Setup

- [VSCode](https://code.visualstudio.com/) + [Volar](https://marketplace.visualstudio.com/items?itemName=johnsoncodehk.volar)
