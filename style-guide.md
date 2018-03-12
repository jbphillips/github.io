---
layout: default
---

## LESS Coding Guidelines
The Obvious Corporation uses LESS as its CSS preprocessor. It's helpful to become familiar with its dynamic behavior before reading these guidelines.

# Naming Conventions
Classes and IDs are lowercase with words separated by a dash:

# Right:

.user-profile {}
.post-header {}
#top-navigation {}
# Wrong:

.userProfile {}
.postheader {}
#top_navigation {}
Image file names are lowercase with words separated by a dash:

# Right:

icon-home.png
# Wrong:

iconHome.png
icon_home.png
iconhome.png
Image file names are prefixed with their usage.

# Right:

icon-home.png
bg-container.jpg
bg-home.jpg
sprite-top-navigation.png
# Wrong:

home-icon.png
container-background.jpg
bg.jpg
top-navigation.png
IDs vs. Classes
You should almost never need to use IDs. Broken behavior due to ID collisions are hard to track down and annoying.

# Color Units
When implementing feature styles, you should only be using color variables provided by colors.less.

When adding a color variable to colors.less, using RGB and RGBA color units are preferred over hex, named, HSL, or HSLA values.

# Right:

rgb(50, 50, 50);
rgba(50, 50, 50, 0.2);
# Wrong:

#FFF;
#FFFFFF;
white;
hsl(120, 100%, 50%);
hsla(120, 100%, 50%, 1);
# z-index scale
Please use the z-index scale defined in z-index.less. @z-index-1 - @z-index-9 are provided. @z-index-9 is the kill -9 of our z-index scale and really should never be used.

# Font Weight
With the additional support of web fonts font-weight plays a more important role than it once did. Different font weights will render typefaces specifically created for that weight, unlike the old days where bold could be just an algorithm to fatten a typeface. Obvious uses the numerical value of font-weight to enable the best representation of a typeface. The following table is a guide:

Raw font weights should not be specified. Instead, use the appropriate font mixin:  .wf-sans-i7, .wf-sans-n7, etc.

The suffix defines the weight and style:

n = normal
i = italic
4 = normal font-weight
7 = bold font-weight
Refer to type.less for type size, letter-spacing, and line height. Raw sizes, spaces, and line heights should be avoided outside of type.less.

ex:

@type-micro
@type-smallest
@type-smaller
@type-small
@type-base
@type-large
@type-larger
@type-largest
@type-jumbo
See Mozilla Developer Network — font-weight for further reading.