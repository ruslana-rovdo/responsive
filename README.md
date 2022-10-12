<h1 align="center">Responsive 📐</h1>

<p align="center">
  <img src="https://img.shields.io/tokei/lines/github/sineylo/responsive?color=6CBA41&style=for-the-badge" alt="Lines of code">
  <img src="https://img.shields.io/github/languages/code-size/SineYlo/responsive?color=6CBA41&style=for-the-badge" alt="Code size">
  <img src="https://img.shields.io/github/repo-size/SineYlo/responsive?color=6CBA41&style=for-the-badge" alt="GitHub repo size">
  <img src="https://img.shields.io/github/languages/top/SineYlo/responsive?color=6CBA41&style=for-the-badge" alt="GitHub top language">
  <img src="https://img.shields.io/github/license/SineYlo/responsive?color=6CBA41&style=for-the-badge" alt="GitHub license">
</p>

<p align="center">
  <b>This formula will help you create cool responsive websites</b>
</p>

<p align="center">
  <a href="https://github.com/SineYlo/responsive/blob/master/README-RU.md">README in Russian</a>
</p>

## 📜 A little about the history of creation

I honestly admit that doing adaptive is a sore topic for me, and I don't really like doing all this. Because it's long and difficult. Therefore, I am constantly looking for something that would simplify this task. You can say there is a `Bootstrap` and you are right. But it's worth remembering how many layouts it uses. If I'm not mistaken, there are about five of them, and the last one already stretches across the entire width. Now let's remember the reality in which we are given at best only 3 different layout options, and at worst only one. Therefore, we must somehow get out of it and come up with something. The meaning of the formula that I developed is that when the screen shrinks, the element will also gradually shrink to the size that you specify in the formula. Yes, this does not solve the problem of using media queries, but I did not say that this is a solution for all occasions. This is just an aid in the implementation of the adaptive, nothing more.

## ⚖️ Types of formula

In total, 2 types of formulas were created. To increase and decrease. Actually, no more is needed. Initially, there was only one view, it was for a decrease, but I realized after some time that this was not enough and after a little brainstorming I created 2 views, for an increase. The formula for decreasing works so that when you compress the site, the size of the element will decrease, and for increasing it will increase. In general, it all sounds logical, but it had to be said, otherwise people are different, they may not understand it that way. The formula works with both the `Desktop First` and `Mobile First` approach. The only thing is if you use it with `Mobile First`, you will have to rebuild your thinking a little, because initially it still went with the expectation of `Desktop First`.

## 📉 Formula for decrease
```
(100vw - var(--responsive-layout-1)) / ((var(--desktop-layout) - var(--responsive-layout-2)) / (var(--desktop-size-1) - var(--mobile-size-1))) + var(--mobile-size-2)
```
1. `desktop-layout` - the width of the container on the desktop without units of measurement (example: 1600).
2. `responsive-layout-1` - the width of the container with the units of measurement to which the compression will take place (example: 320px).
3. `responsive-layout-2` - the same value as in the previous variable, but without units of measurement (example: 320).
4. `desktop-size-1` - the size of the element on the desktop without units of measurement (example: 80).
5. `desktop-size-2` - the same value as in the previous variable, but with units of measurement (example: 80px).
6. `mobile-size-1` - the final value of the size without units of measurement to which we need to compress the element (example: 15).
7. `mobile-size-2` - the same value as in the previous variable, but with units of measurement (example: 15px).

### Usage example
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
## 📈 Formula for increase
```
var(--mobile-size-2) - (100vw - var(--responsive-layout-1)) / ((var(--desktop-layout) - var(--responsive-layout-2)) / (var(--mobile-size-1) - var(--desktop-size-1)))
```
1. `desktop-layout` - the width of the container on the desktop without units of measurement (example: 1600).
2. `responsive-layout-1` - the width of the container with the units of measurement to which the compression will take place (example: 320px).
3. `responsive-layout-2` - the same value as in the previous variable, but without units of measurement (example: 320).
4. `desktop-size-1` - the size of the element on the desktop without units of measurement (example: 30).
5. `desktop-size-2` - the same value as in the previous variable, but with units of measurement (example: 30px).
6. `mobile-size-1` - the final value of the size without units of measurement to which we need to increase the element (example: 80).
7. `mobile-size-2` - the same value as in the previous variable, but with units of measurement (example: 80px).

### Usage example
```
.box {
  /* Responsive font-size */
  --desktop-layout: 1600;
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

## 🔮 What is important to know
- The example uses the `font-size` property, but this does not mean that this formula is suitable only for this property. It is generally suitable for almost any property that has dimensions.
- In this formula, other units of measurement are allowed instead of pixels. You can conditionally use `rem` if you want to. There are no restrictions here.
- In the `responsive.css` file, I have prepared examples of using this formula, and so in general it is not needed for work.
- The `responsive.scss` file contains two functions (for decreasing and increasing) that you can apply to any properties that support dimensions. Ideally, use this formula through functions, because if you write, as in the CSS example, then the file will be bloated and it will also weigh a lot, which is not very good. Also, if desired, you can use the fifth parameter `unit`, thereby replacing the unit `vw` with `vh`.

## 🔱 Created with the support of

<a href="https://www.browserstack.com">
  <img src="temp/logo-browserstack.svg?sanitize=false" width="200" alt="browserstack">
</a>

## 📃 What is used in this repository
- Semantic versioning - [semver.org](https://semver.org)
- Conventional commits - [conventionalcommits.org](https://www.conventionalcommits.org/en/v1.0.0/)
