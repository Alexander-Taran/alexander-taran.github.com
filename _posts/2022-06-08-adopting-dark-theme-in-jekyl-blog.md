---
layout: post
title: "How to make your Jekyl blog respect users theme (dark or light)"
---

Late night browsing. Lights are off. Going to read some github pages built with Jekyll with default theme. So bright!

We got so used to automatic theme switching on our devices.  
CSS supports themes with [`prefers-color-scheme`](https://developer.mozilla.org/en-US/docs/Web/CSS/@media/prefers-color-scheme).  
With decent support in browsers.  

![](/assets/images/can-i-use-prefers-color-scheme.png)

Yet most of the sites don't utilize the power of it.

> if you don't have minima theme copied to your site's source you can find it in [minima theme repository](https://github.com/jekyll/minima)

Here is how you can update your Jekyll site (most of github pages) to respect your visitors:

Update `styles/css/style.scss` like this
```scss
--- 
# Only the main Sass file needs front matter (the dashes are enough) 
---

// We import the light theme first.
@import "minima/skins/classic";

// We define css variables based on theme color
:root {
  --brand-color :           #{$brand-color};
  --brand-color-light :     #{$brand-color-light};
  --brand-color-dark :      #{$brand-color-dark};

  --site-title-color :      #{$site-title-color};

  --text-color :            #{$text-color};
  --background-color :      #{$background-color};
  --code-background-color : #{$code-background-color};

  --link-base-color:        #{$link-base-color};
  --link-visited-color:     #{$link-visited-color};
  --link-hover-color:       #{$link-hover-color};

  --border-color-01:        #{$border-color-01};
  --border-color-02:        #{$border-color-02};
  --border-color-03:        #{$border-color-03};

  --table-text-color:       #{$table-text-color};
  --table-zebra-color:      #{$table-zebra-color};
  --table-header-bg-color:  #{$table-header-bg-color};
  --table-header-border:    #{$table-header-border};
  --table-border-color:     #{$table-border-color};
}

// now we redefive those variables to use css variables with a fallback
$brand-color:           var(--brand-color,$brand-color); 
$brand-color-light:     var(--brand-color-light,$brand-color-light); 
$brand-color-dark:      var(--brand-color-dark,$brand-color-dark); 

$site-title-color:      var(--site-title-color,$site-title-color);

$text-color:            var(--text-color,$text-color);
$background-color:      var(--background-color,$background-color);
$code-background-color: var(--background-color,$code-background-color);

$link-base-color:       var(--link-base-color,$link-base-color);
$link-visited-color:    var(--link-visited-color,$link-visited-color);
$link-hover-color:      var(--link-hover-color,$link-hover-color);

$border-color-01:       var(--border-color-01,$border-color-01);
$border-color-02:       var(--border-color-02,$border-color-02);
$border-color-03:       var(--border-color-03,$border-color-03);

$table-text-color:      var(--table-text-color,$table-text-color);
$table-zebra-color:     var(--table-zebra-color,$table-zebra-color);
$table-header-bg-color: var(--table-header-bg-color,$table-header-bg-color);
$table-header-border:   var(--table-header-border,$table-header-border);
$table-border-color:    var(--table-border-color,$table-border-color);

// now we proceed with minima
@import "minima/initialize";


// define media query for dark theme users
@media (prefers-color-scheme: dark) {

// Import dark skin
// We will have to alter it as well
// It gives our variables new meaning yet again
// but you have to remove  "!default" a the end of declarations.
  @import "minima/skins/dark";

  :root {
    --brand-color :           #{$brand-color};
    --brand-color-light :     #{$brand-color-light};
    --brand-color-dark :      #{$brand-color-dark};
  
    --site-title-color :      #{$site-title-color};
  
    --text-color :            #{$text-color};
    --background-color :      #{$background-color};
    --code-background-color : #{$code-background-color};
  
    --link-base-color:        #{$link-base-color};
    --link-visited-color:     #{$link-visited-color};
    --link-hover-color:       #{$link-hover-color};
  
    --border-color-01:        #{$border-color-01};
    --border-color-02:        #{$border-color-02};
    --border-color-03:        #{$border-color-03};
  
    --table-text-color:       #{$table-text-color};
    --table-zebra-color:      #{$table-zebra-color};
    --table-header-bg-color:  #{$table-header-bg-color};
    --table-header-border:    #{$table-header-border};
    --table-border-color:     #{$table-border-color};
  }
}
```

Chrome can emulate users theme preferences in developer tools  

![](/assets/images/theme-preference-emulation.png)

You can find in [this commit](https://github.com/Alexander-Taran/alexander-taran.github.com/commit/dd8dcf59fa2eb596f71c315f32fee679dd2511d3)

No go and adopt dark theme support.

