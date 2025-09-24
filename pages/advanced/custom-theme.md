# 新增单个转发
<img width="1008" height="966" alt="image" src="https://github.com/user-attachments/assets/c6b72f20-2482-45be-a462-a52c7f216c05" />

监听端口 - 支持三种格式88 88/udp 88/tcp，如果不带协议，默认是tcp，多个端口以空格分隔
源IP - 目录仅支持IP，不支持域名
源端口 - 任意端口
## 批量添加转发
<img width="1020" height="914" alt="image" src="https://github.com/user-attachments/assets/9b91bc6b-d7ed-4c1e-b662-348e2fa3725b" />

格式为: 监听端口|IP|回源端口
如：
88 99|1.2.3.4|8080
88/tcp 99/udp|1.2.3.4|8080

## 监听设置
<img width="1806" height="314" alt="image" src="https://github.com/user-attachments/assets/6bdc1093-3c54-49cf-bbd3-dbbead6f570c" />
可删除或添加监听端口

源站设置

单IP连接数限制
<img width="1172" height="218" alt="image" src="https://github.com/user-attachments/assets/de745bce-1f21-4ad6-acd1-512aac6f1dcc" />
限制单个IP同时发起的连接数限制

ACL
<img width="3198" height="492" alt="image" src="https://github.com/user-attachments/assets/0e6873c4-38fc-427b-9530-c4f4d958aa18" />

### Basic Theme Setup

Create a theme directory structure:

```
.vitepress/
├── theme/
│   ├── index.ts
│   ├── style.css
│   └── components/
│       └── CustomComponent.vue
└── config.ts
```

### Theme Entry Point

Create `.vitepress/theme/index.ts`:

```ts
import { h } from 'vue'
import DefaultTheme from 'vitepress/theme'
import './style.css'

export default {
  ...DefaultTheme,
  Layout: () => {
    return h(DefaultTheme.Layout, null, {
      // Override slots here
    })
  },
  enhanceApp({ app }) {
    // Register custom components
    // app.component('MyComponent', MyComponent)
  }
}
```

### Custom Styles

Add your custom CSS in `.vitepress/theme/style.css`:

```css
:root {
  --vp-c-brand: #646cff;
  --vp-c-brand-light: #747bff;
  --vp-c-brand-dark: #535bf2;
}

/* Custom component styles */
.custom-component {
  border: 1px solid var(--vp-c-divider);
  border-radius: 8px;
  padding: 16px;
  margin: 16px 0;
}
```

## Theme Customization Options

### Colors

You can customize the color scheme by overriding CSS variables:

```css
:root {
  /* Primary brand color */
  --vp-c-brand: #646cff;
  --vp-c-brand-light: #747bff;
  --vp-c-brand-dark: #535bf2;
  
  /* Background colors */
  --vp-c-bg: #ffffff;
  --vp-c-bg-alt: #f6f6f7;
  
  /* Text colors */
  --vp-c-text-1: #213547;
  --vp-c-text-2: #476582;
  --vp-c-text-3: #8f9198;
}
```

### Typography

Customize fonts and typography:

```css
:root {
  --vp-font-family-base: 'Inter', -apple-system, BlinkMacSystemFont, sans-serif;
  --vp-font-family-mono: 'Fira Code', 'Monaco', 'Consolas', monospace;
}

/* Custom heading styles */
h1 {
  font-size: 2.5rem;
  font-weight: 700;
  line-height: 1.2;
}
```

### Layout Customization

Override layout components:

```ts
import { h } from 'vue'
import DefaultTheme from 'vitepress/theme'
import CustomLayout from './CustomLayout.vue'

export default {
  ...DefaultTheme,
  Layout: () => h(CustomLayout)
}
```

## Advanced Customization

### Custom Components

Create reusable components:

```vue
<!-- Example: .vitepress/theme/components/InfoBox.vue -->
<template>
  <div class="info-box" :class="type">
    <div class="icon">{{ icon }}</div>
    <div class="content">
      <h4>{{ title }}</h4>
      <p>{{ content }}</p>
    </div>
  </div>
</template>

<script setup>
defineProps({
  type: {
    type: String,
    default: 'info'
  },
  title: String,
  content: String,
  icon: String
})
</script>

<style scoped>
.info-box {
  display: flex;
  padding: 16px;
  border-radius: 8px;
  margin: 16px 0;
}

.info-box.info {
  background: #e3f2fd;
  border: 1px solid #2196f3;
}

.info-box.warning {
  background: #fff3e0;
  border: 1px solid #ff9800;
}
</style>
```

### Global Components

Register components globally:

```ts
// .vitepress/theme/index.ts
import InfoBox from './components/InfoBox.vue'

export default {
  ...DefaultTheme,
  enhanceApp({ app }) {
    app.component('InfoBox', InfoBox)
  }
}
```

## Best Practices

### Performance

- Keep custom CSS minimal and focused
- Use CSS variables for consistent theming
- Avoid heavy JavaScript in theme components

### Accessibility

- Maintain proper color contrast ratios
- Ensure keyboard navigation works
- Test with screen readers

### Responsive Design

- Test on different screen sizes
- Use relative units (rem, em, %)
- Implement mobile-first design

## Examples

Here's an example of how to use custom components in your theme:

```js
// In your Vue component
<template>
  <div class="custom-info-box">
    <div class="icon">💡</div>
    <div class="content">
      <h4>Theme Customization</h4>
      <p>VitePress themes are highly customizable and can be extended with Vue components.</p>
    </div>
  </div>
</template>
```

This demonstrates how custom components can be integrated into your VitePress theme. 
