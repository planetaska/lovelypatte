---
layout: default
author: aska

---
# Add TailwindUI to Rails 6 application

This article is for:

    ruby '3.0.1'
    rails '6.1.3.1'

## Install TailwindCSS

Run

`yarn add tailwindcss@latest postcss@latest autoprefixer@latest`

## Create the SCSS files to include TailwindCSS

Create these files and directory:

This will be the import file:

`./app/javascript/stylesheets/application.scss`

This will be where you can add custom styles:

`./app/javascript/stylesheets/custom.scss`

And in application.scss:

    @import "~tailwindcss/base";
    @import "~tailwindcss/components";
    @import "~tailwindcss/utilities";
    
    @import "custom";

The custom.scss is where you add your custom styles.

## Create TailwindCSS config file

Run

`npx tailwindcss init`

This will create a tailwind.config.js file at the root of the rails app.

### Optional: move the config file

Move the created tailwind.config.js to somewhere like:

`/app/javascript/stylesheets/tailwind.config.js`

Then tell the PostCSS where to find the config file:

    module.exports = {
      plugins: [
        require('tailwindcss')('./app/javascript/stylesheets/tailwind.config.js'),
        require('postcss-import'),
        require('postcss-flexbugs-fixes'),
        require('postcss-preset-env')({
          autoprefixer: {
            flexbox: 'no-2009'
          },
          stage: 3
        })
      ]
    }

### Optional: include Inter font

Add to application layout:

    <link rel="stylesheet" href="https://rsms.me/inter/inter.css">

## Install TailwindUI first-party plugins

`yarn add @tailwindcss/forms @tailwindcss/typography @tailwindcss/aspect-ratio`

Then include these plugins, the font, and the purge CSS rule in the Tailwind config file:

    const defaultTheme = require('tailwindcss/defaultTheme')
    
    module.exports = {
      future: {
        purgeLayersByDefault: true
      },
      mode: 'jit',
      purge: [
        './app/**/*.html.erb',
        './app/helpers/**/*.rb',
        './app/javascript/**/*.js'
      ],
      theme: {
        extend: {
          fontFamily: {
            sans: ['Inter var', ...defaultTheme.fontFamily.sans],
          },
        },
      },
      variants: {},
      plugins: [
        require('@tailwindcss/forms'),
        require('@tailwindcss/typography'),
        require('@tailwindcss/aspect-ratio'),
      ],
    }

## Finally, include the styles with pack_tag

In application layout, add:

    <%= stylesheet_pack_tag 'application', media: 'all', 'data-turbolinks-track': 'reload' %>

And that's it!