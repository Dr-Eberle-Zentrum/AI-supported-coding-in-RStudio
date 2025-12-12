# UT Varnish Fork Setup Instructions

To implement UT branding with minimal maintenance burden, create a minimal fork of carpentries/varnish that only overrides color variables.

## Quick Setup

1. **Fork the varnish repository**:
   - Go to https://github.com/carpentries/varnish
   - Click "Fork" and create it under `Dr-Eberle-Zentrum/varnish`

2. **Update the color variables**:
   - Edit `source/stylesheets/variables.scss`
   - Change the following color variables:

```scss
// UT Brand Colors (add these after the existing color definitions)
$ut-red: #A51E37;
$ut-red-light: #ffd9e0;
$ut-red-dark: #a82a41;
```

3. **Update header.scss**:
   - Edit `source/stylesheets/header.scss`
   - Add UT-specific progress bar styling after existing carpentry styles:

```scss
// UT (University of Tübingen) styling
.bottom-nav.UT {
  border-top: 45px solid $ut-red;
}

.progress.UT {
  background: $ut-red-light;
}

.progress-bar.UT {
  background: $ut-red-dark;
}
```

4. **Build the CSS** (if you want to test locally):
   ```bash
   bash squash-sass.sh
   ```
   
   Or let GitHub Actions build it automatically when you push.

5. **Update your lesson's config.yaml**:
   ```yaml
   varnish: Dr-Eberle-Zentrum/varnish
   ```

## Alternative: Use CSS Variables

If you want an even simpler approach that doesn't require a fork, you can use CSS custom properties (variables) in your `files/ut-branding.css`:

```css
:root {
  --ut-primary: #A51E37;
  --ut-light: #ffd9e0;
  --ut-dark: #a82a41;
}
```

However, this still requires a mechanism to inject the CSS into the page, which the current Workbench doesn't support out-of-the-box.

## Recommended Approach

For now, using an updated fork of varnish is the most practical solution:

1. It maintains compatibility with upstream
2. Only requires updating the fork when new varnish releases add features you need
3. Provides full control over branding
4. Works automatically with the Workbench build system

The fork only needs to change ~10 lines of code (color variables and carpentry-specific selectors), making it easy to merge upstream updates when needed.

## Files in this Directory

The `ut-branding.css` file in this directory contains the standalone CSS that would be applied. It can serve as a reference for what colors to use in your varnish fork.
