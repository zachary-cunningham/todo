# Design Standards

**Status:** AI-generated | Approved for v0.1 to `01_core_constraints/`. Will need a review on what can be reduced/simplfied later.

**Purpose:** Immutable design system. All UI components must reference these exact values. No arbitrary colors, spacing, or sizes permitted.

---

## Typography

### Font Family
- **Primary:** System font stack (iOS: SF Pro, Android: Roboto)
- **Monospace:** System monospace (iOS: SF Mono, Android: Roboto Mono)

### Font Sizes
```
FONT_HEADING: 24px
FONT_TITLE: 18px
FONT_BODY: 15px
FONT_DETAIL: 13px
FONT_CAPTION: 11px
```

### Font Weights
```
WEIGHT_REGULAR: 400
WEIGHT_MEDIUM: 500
WEIGHT_SEMIBOLD: 600
```

---

## Color Palette

### Core Colors
```
COLOR_BACKGROUND: #FFFFFF
COLOR_SURFACE: #F7F7F5
COLOR_BORDER: #E3E3E0
COLOR_TEXT_PRIMARY: #37352F
COLOR_TEXT_SECONDARY: #6F6F6F
COLOR_TEXT_TERTIARY: #9B9B9B
COLOR_ICON: #37352F (opacity 0.45)
```

### Interactive Colors
```
COLOR_PRIMARY: #2383E2
COLOR_PRIMARY_HOVER: #1A6DC4
COLOR_DESTRUCTIVE: #E03E3E
COLOR_SUCCESS: #0F7B6C
COLOR_CHECKBOX_CHECKED: #37352F
COLOR_CHECKBOX_UNCHECKED: #E3E3E0
```

### Overlay
```
COLOR_OVERLAY: #000000 (opacity 0.3)
COLOR_POPUP_BACKGROUND: #FFFFFF
COLOR_POPUP_SHADOW: #000000 (opacity 0.1)
```

---

## Spacing Scale

Use only these values for margins, padding, gaps:

```
SPACE_XXS: 4px
SPACE_XS: 8px
SPACE_SM: 12px
SPACE_MD: 16px
SPACE_LG: 24px
SPACE_XL: 32px
SPACE_XXL: 48px
```

---

## Layout

### Screen Padding
```
SCREEN_PADDING_HORIZONTAL: 16px
SCREEN_PADDING_VERTICAL: 12px
```

### Component Dimensions
```
TODO_ITEM_HEIGHT: 44px (minimum touch target)
CHECKBOX_SIZE: 20px
ICON_SIZE_SM: 16px
ICON_SIZE_MD: 20px
ICON_SIZE_LG: 24px
POPUP_WIDTH: 90% of screen width (max 400px)
POPUP_BORDER_RADIUS: 8px
SWIPE_THRESHOLD: 80px (distance to trigger action)
```

### Separator
```
SEPARATOR_HEIGHT: 1px
SEPARATOR_COLOR: COLOR_BORDER
```

---

## Gesture Interactions

### Swipe Left (Delete)
- Background color: `COLOR_DESTRUCTIVE`
- Swipe distance to trigger: `SWIPE_THRESHOLD`
- Animation: 200ms ease-out

### Swipe Right (Edit)
- Background color: `COLOR_PRIMARY`
- Swipe distance to trigger: `SWIPE_THRESHOLD`
- Animation: 200ms ease-out

### Tap (Checkbox)
- Active state: scale 0.95
- Animation: 150ms ease-in-out
- Checkbox transition: 200ms

### Info Icon (Show Details)
- Appears when todo is in edit mode
- Position: absolute right, vertically centered
- Size: `ICON_SIZE_MD`
- Color: `COLOR_ICON`

---

## Component States

### Todo Item
- **Default:** Background `COLOR_BACKGROUND`, text `COLOR_TEXT_PRIMARY`
- **Completed:** Text strikethrough, `COLOR_TEXT_TERTIARY`, pushed to bottom of list
- **Active/Editing:** Background `COLOR_SURFACE`, cursor visible
- **Swipe hint:** Subtle shadow during gesture

### Popup Card (Info Detail)
- Background: `COLOR_POPUP_BACKGROUND`
- Shadow: `COLOR_POPUP_SHADOW`, offset (0, 4px), blur 12px
- Border radius: `POPUP_BORDER_RADIUS`
- Padding: `SPACE_LG`

---

## Animation Standards

All animations must use these exact durations:

```
ANIM_FAST: 150ms
ANIM_STANDARD: 200ms
ANIM_SLOW: 300ms
EASING_DEFAULT: ease-in-out
```

---

## Immutable Rules

1. **No custom colors** — Only palette colors permitted
2. **No arbitrary spacing** — Only spacing scale values permitted
3. **Consistent typography** — Only defined font sizes/weights
4. **Touch targets** — Minimum 44px for all interactive elements
5. **Gesture consistency** — Left always delete, right always edit
