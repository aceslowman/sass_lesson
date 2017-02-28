# SASS

## What is SASS?

SASS (Syntactically Awesome Stylesheets) is a CSS preprocessor that allows us to create more modular, more readable, and more usable CSS.

## Why use SASS?

You might have been in the situation where your CSS file has become bloated and unmanageable. Rarely does straight CSS lend well to a well organized project.

Say your site has a few colors you use often. A primary color, a secondary color, and then an accent color. With CSS, you have to look for the right hex value and change *each and every one of them manually*.

We should all know that, as coders, we *don't want to do the same thing twice*. This should be a rule we live by, and CSS is painful for this reason. SASS seeks to introduce more elegant syntax to your workflow.

## Let's use SASS

SASS uses .scss files and compiles them down into optimized .css files, so for this, we will need to install SASS on your machine.

**NOTE:** To install SASS on a Windows machine, you must already have Ruby installed. Use the [Ruby Installer](http://rubyinstaller.org/) here before we begin.

### Installation

1. Open up the Terminal or Command Prompt.

2. Use Gem to install SASS. (Gem is a package manager for the Ruby language)

```
gem install sass
```

or

```
sudo gem install sass
```

*(You can be sure it's installed correctly by running `sass -v` in your terminal)*

3. Now we can begin writing our first .scss file and compile it to .css.

### Syntax

SASS is most immediately different from CSS in three ways:

1. Nesting
2. Variables
3. Mixins

#### Nesting

Nesting is one of my favorite features. In any project, you will see a lot of this in CSS:

```
.someClass ul {

}

.someClass ul li{

}

.someClass ul li a{

}

.someClass ul li a:hover{

}

.someClass ul li a:active{

}
```

This is difficult to read in a long stylesheet. What you get to do here is *nest* in SASS.

```
.someClass{
  ul{
    li{
      a{
        &:hover{

        }
        &:active{

        }
      }
    }
  }
}
```

And now, when we are looking for where to style a specific anchor tag, deep within "someClass", we can search *much* more efficiently.

---

When I begin a new project, I might start with straight CSS. I'll try to keep it organized, but more than anything, I'm *sketching*. To stay organized, you have to move out of the phase, and often I begin by organizing my straight CSS into SASS by nesting.

---

#### Variables

As programmers, we all know the great feeling of changing something in one place, and having that change reflected in many places.

A great example is color schemes. If you have a carefully chosen set of colors, you can use SASS to manage them much more efficiently.

Instead of:

```
.someClass-1{
  background-color:#111;
}

.someClass-1 a{
  color: #333;
}

.someClass-2{
  background-color:#111;
  border: 1px solid #222;
}
```

You can use:

```
$primary-color: #111;
$secondary-color: #222;
$accent-color: #333;

.someClass-1{
  background-color: $primary-color;
  a{
    color: $accent-color;
  }
}

.someClass-2{
  background-color: $primary-color;
  border: 1px solid $secondary-color;
}
```

#### Mixins

Mixins aid in making your CSS more modular and reusable. They are essentially pieces of css that you can include in other classes, and can accept arguments.

A typical example might be a mixin to handle your link colors.

```
@mixin links ($link, $visited, $hover, $active) {
    & {
        color: $link;
        &:visited {
            color: $visited;
        }
        &:hover {
            color: $hover;
        }
        &:active, &:focus {
            color: $active;
        }
    }
}
```

This can be used like this:

```
.someClass-1{
  a{
    @include links(red, green, blue, orange);
  }
}
.someClass-2{
  a{
    @include links(orange, green, blue, red);
  }
}
```

Now it is much easier to organize and read.

### Compiling to CSS

A .scss file by itself is not useful to the browser. SASS will compile these files to a .css file when you run the following command in Terminal or Command Prompt:

```
sass input.scss output.css
```

Now, your scss file will be compiled into a new css file, named output. There are several ways you can optimize this output, but you can find those options using `sass -h`.

This is useful, but you probably don't want to run this command every time you make a change to the .scss file. You can use the following command to tell SASS to watch for changes:

```
sass --watch scss:css
```

This command will watch the /scss folder in your project for any changes, and will automatically output the compiled css in the /css folder.

You are ready to start using SASS!
