# Custom UT Branding

This directory contains custom styling files for University of Tübingen (UT) branding.

## Files

- `ut-branding.css` - Custom CSS with UT color overrides
- `VARNISH_FORK_INSTRUCTIONS.md` - Step-by-step guide for creating a minimal varnish fork

## UT Brand Colors

The UT branding uses the following colors:
- **Primary Red**: `#A51E37` - Used for navigation borders
- **Light Red/Pink**: `#ffd9e0` - Used for progress bar background  
- **Dark Red**: `#a82a41` - Used for progress bar foreground

These replace the default Carpentries Workbench colors (blues and purples).

## Current Limitations

The Carpentries Workbench (sandpaper + varnish) has limited built-in support for custom CSS without forking the varnish template package. The `ut-branding.css` file provides the necessary color overrides, but it requires one of the following approaches to be applied:

### Option 1: Fork varnish (Recommended for full integration)

Create a fork of the carpentries/varnish repository and:
1. Update `source/stylesheets/variables.scss` with UT colors
2. Build the CSS/JS assets
3. Point `config.yaml` to your fork: `varnish: Dr-Eberle-Zentrum/varnish`

This was the original approach used, but it requires maintaining the fork up-to-date with upstream changes.

### Option 2: Manual CSS injection (Current workaround)

The `ut-branding.css` file can be manually added to the built site after generation, but this needs to be done after each build and won't persist in the git repository.

### Option 3: Custom varnish with UT carpentry type

Extend varnish to recognize 'UT' as a carpentry type with its own color scheme. This would require:
1. Adding UT favicon files to `inst/pkgdown/assets/favicons/UT/`
2. Adding UT-specific styles to the SCSS files
3. Submitting this as a contribution to carpentries/varnish

## Future Enhancement

The ideal solution would be for the Carpentries Workbench to support a `custom_css` configuration option in `config.yaml`, allowing lessons to easily override colors without forking varnish. Consider opening an issue or discussion in the carpentries/sandpaper repository to request this feature.

## Related Links

- [Carpentries Varnish](https://github.com/carpentries/varnish)
- [Carpentries Sandpaper](https://github.com/carpentries/sandpaper)
- [UT Corporate Design](https://uni-tuebingen.de/en/facilities/administration/v-kommunikation-und-marketing/corporate-design/)
