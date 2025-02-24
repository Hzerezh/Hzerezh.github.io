# Шпаргалка по Telegram Mini Apps 

## Подключение

Подключение в шапке:
```html
<script src="https://telegram.org/js/telegram-web-app.js"></script>
```

## Использование
В js скрипте
```js
window.Telegram.WebApp.         // переменная через window

Telegram.WebApp.ready()         // переменная без window
```

CSS
```css
var(--tg-theme-bg-color)
var(--tg-theme-text-color)
var(--tg-theme-hint-color)
var(--tg-theme-link-color)
var(--tg-theme-button-color)
var(--tg-theme-button-text-color)
var(--tg-theme-secondary-bg-color)
var(--tg-theme-header-bg-color)
var(--tg-theme-bottom-bar-bg-color)
var(--tg-theme-accent-text-color)
var(--tg-theme-section-bg-color)
var(--tg-theme-section-header-text-color)
var(--tg-theme-section-separator-color)
var(--tg-theme-subtitle-text-color)
var(--tg-theme-destructive-text-color)
```