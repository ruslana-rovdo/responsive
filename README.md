# Responsive.css 📐
![Lines of code](https://img.shields.io/tokei/lines/github/sineylo/Responsive.css?style=for-the-badge) ![Code size](https://img.shields.io/github/languages/code-size/SineYlo/Responsive.css?style=for-the-badge) ![GitHub repo size](https://img.shields.io/github/repo-size/SineYlo/Responsive.css?style=for-the-badge) ![GitHub](https://img.shields.io/github/license/SineYlo/Responsive.css?style=for-the-badge)  

> Formula to help you make cool responsive websites

## 📜 A little about how this formula was developed and what it is for:
I honestly admit that adaptive websites are a sore subject for me, and I don't really like doing it. Because it is long and difficult. Therefore, I am constantly on the lookout for something that would simplify this task. You can say there is Bootstrap and you are right. But it's worth remembering how many layouts are used in it. If I’m not mistaken, it’s about five, and the last one already stretches across the entire width. Now let's remember the reality where we are given only 3 different layout options at best, and at worst only two. Therefore, we have to somehow get out and come up with something. This formula, which I developed, is that when the screen shrinks, the blocks will be at the end of the dimensions that you specify in the formula. Yes, this does not solve the issue of using media queries, but I did not say that this is a solution for all occasions. This is just a help in implementing responsive design, nothing more.

## ⚙️ How the reduction formula works and what it consists of:

```
(100vw - var(--responsive-layout-1)) / ((var(--desktop-layout) - var(--responsive-layout-2)) / (var(--desktop-size-1) - var(--mobile-size-1))) + var(--mobile-size-2)
```

1. `desktop-layout` - in this variable we specify the size of our container on the desktop (for example: 768px).
2. `responsive-layout-1` - in this variable we specify the size of the container to which the compression will occur (for example: 320px) (IMPORTANT! In this variable, we specify the value strictly with the units of measurement (this is possible - 320px, and so - 320 is not possible)).
3. `responsive-layout-2` - in this variable we specify the same value as in `responsive-layout-1`, but without px this is important.
4. `desktop-size-1` - in this variable we indicate what size of the font or block on the desktop version (example: 80) (IMPORTANT! Here we indicate the value without units of measurement).
5. `desktop-size-2` - this variable is not used in the formula, but we will need it later in the font-size property (example: 80px) (IMPORTANT! Here we specify the value with a unit of measurement).
6. `mobile-size-1` - in this variable we indicate the size of the font or block on the mobile version (example: 15) (IMPORTANT! Here we indicate the value without units of measurement).
7. `mobile-size-2` - in this variable we also indicate the value of the font or block on the mobile version, but with the units of measurement (example: 15px).

## 🛠 Writing a formula for reduction:

```
.box {
  /* Responsive font-size */
  --desktop-layout: 1600;
  --responsive-layout-1: 320px;
  --responsive-layout-2: 320;
  --desktop-size-1: 80;
  --desktop-size-2: 80px;
  --mobile-size-1: 15;
  --mobile-size-2: 15px;
  --responsive-size: (100vw - var(--responsive-layout-1)) / ((var(--desktop-layout) - var(--responsive-layout-2)) / (var(--desktop-size-1) - var(--mobile-size-1))) + var(--mobile-size-2);
  font-size: clamp(var(--mobile-size-2), var(--responsive-size), var(--desktop-size-2));
}
```
## ⚙️ How does the enlargement formula work and what does it consist of:

```
var(--mobile-size-2) - (100vw - var(--responsive-layout-1)) / ((var(--desktop-layout) - var(--responsive-layout-2)) / (var(--mobile-size-1) - var(--desktop-size-1)))
```

This formula was added in the new `2.0` update.  
All you need is to specify the minimum font size in the `--desktop-size` variable, and the maximum in `--mobile-size`.  
Well, in font-size, swap `--desktop-size` and `--mobile-size` in the clamp function.

If with that formula, when the screen narrowed, the font decreased (i.e., from 80 on the desktop it became 30 on the mobile), now the font, on the contrary, increases (i.e., from 30 on the desktop to 80 on the mobile).

## 🛠 Writing a formula for increasing:

```
.box {
  /* Responsive font-size to increase */
  --desktop-layout: 1950;
  --responsive-layout-1: 320px;
  --responsive-layout-2: 320;
  --desktop-size-1: 30;
  --desktop-size-2: 30px;
  --mobile-size-1: 80;
  --mobile-size-2: 80px;
  --responsive-size: var(--mobile-size-2) - (100vw - var(--responsive-layout-1)) / ((var(--desktop-layout) - var(--responsive-layout-2)) / (var(--mobile-size-1) - var(--desktop-size-1)));
  font-size: clamp(var(--desktop-size-2), var(--responsive-size), var(--mobile-size-2));
}
```
## ❗️ ATTENTION:

- This formula works, as in the desktop-first approach, and in the mobile-first approach, the formula does not change from this. The only thing you need is not only one layout option, but at least two (initial and final). Because in the formula you write two values, which is logical from and to.
- In the description, I mainly mentioned font size, but in fact, this formula applies to anything that will change sizes. For example, the width and height of a button or block of some kind. There is no difference, it's just that I mostly use it for font size and padding.
- Also, in this formula, other units of measurement are allowed instead of px. You can use `em`, `rem` whatever you like. There are no restrictions here.
- An important point if you want to use this formula for many css properties at once, look in the `responsive.css` file there I prepared different variants of variables for the main properties.
- For those who already use the `SCSS` preprocessor there is a ready-made file with mixins. All you need to do is simply connect and use.

## 💎 With the support of:

<a href="https://www.browserstack.com">
  <img src="temp/Browserstack-logo.svg?sanitize=false" alt="browserstack" width="160">
</a> 

***

If you have any questions or suggestions, you can write to the `issues` section or email me - `contact@sineylo-dev.ru`
