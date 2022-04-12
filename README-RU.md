<h1 align="center">Responsive 📐</h1>

<p align="center">
  <img src="https://img.shields.io/tokei/lines/github/sineylo/responsive?color=6CBA41&style=for-the-badge" alt="Lines of code">
  <img src="https://img.shields.io/github/languages/code-size/SineYlo/responsive?color=6CBA41&style=for-the-badge" alt="Code size">
  <img src="https://img.shields.io/github/repo-size/SineYlo/responsive?color=6CBA41&style=for-the-badge" alt="GitHub repo size">
  <img src="https://img.shields.io/github/languages/top/SineYlo/responsive?color=6CBA41&style=for-the-badge" alt="GitHub top language">
  <img src="https://img.shields.io/github/license/SineYlo/responsive?color=6CBA41&style=for-the-badge" alt="GitHub license">
</p>

<p align="center">
  <b>Данная формула поможет вам создавать крутые отзывчивые сайты</b>
</p>

## 📜 Немного о истории создания

Я честно признаюсь, что делать адаптив больная тема для меня, и мне не очень нравится всем этим заниматься. Потому что это долго и сложно. Поэтому я постоянно нахожусь в поиске чего-то, что упростило бы эту задачу. Вы можете сказать, что есть `Bootstrap`, и вы правы. Но стоит помнить, сколько макетов в нем используется. Если я не ошибаюсь, их около пяти, и последний уже тянется по всей ширине. Теперь давайте вспомним реальность, в которой нам дают в лучшем случае только 3 различных варианта макета, а в худшем — только один. Поэтому мы должны как-то выкручиваться и что-то придумывать. Смысл формулы, которую я разработал, заключается в том, что когда экран сжимается, элемент будет тоже постепенно сжиматься до конечно размера, который вы указываете в формуле. Да, это не решает проблему использования медиа-запросов, но я и не говорил, что это решение на все случаи жизни. Это просто помощь в реализации адаптива, не более того.

## ⚖️ Виды формулы

Всего было создано 2 вида формулы. На увеличение и на уменьшение. Собственно больше и не нужно. Изначально был только один вид это на уменьшение, но я понял через какое-то время, что этого мало и немного пораскинув мозгами создал 2 вид, на увеличение. Формула на уменьшение работает так, что когда вы сжимаете сайт размер элемента будет уменьшаться, а на увеличение - увеличиваться. В целом это всё звучит логично, но нужно было сказать, а то люди разные бывают, могут и не так понять. Формула работает, как с подходом `Desktop First`, так и с `Mobile First`. Единственно если вы будете её использовать с `Mobile First` немного придется перестроить мышление ибо изначально она всё-таки шла с расчётом на `Desktop First`.

## 📉 Формула на уменьшение
```
(100vw - var(--responsive-layout-1)) / ((var(--desktop-layout) - var(--responsive-layout-2)) / (var(--desktop-size-1) - var(--mobile-size-1))) + var(--mobile-size-2)
```
1. `desktop-layout` - ширина контейнера на десктопе без единиц измерения (пример: 1600).
2. `responsive-layout-1` - ширина контейнера с единицами измерения, до которого будет происходить сжатие (пример: 320px).
3. `responsive-layout-2` - то же значение, что и в прошлой переменной, но уже без единиц измерения (пример: 320).
4. `desktop-size-1` - размер элемента на десктопе без единиц измерения (пример: 80).
5. `desktop-size-2` - то же значение, что и в прошлой переменной, но уже с единицами измерения (пример: 80px).
6. `mobile-size-1` - конечное значение размера без единиц измерения, до которого нам нужно сжать элемент (пример: 15).
7. `mobile-size-2` - то же значение, что и в прошлой переменной, но уже с единицами измерения (пример: 15px).

### Пример использования
```
.box {
  /* Отзывчивый font-size */
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
## 📈 Формула на увеличение
```
var(--mobile-size-2) - (100vw - var(--responsive-layout-1)) / ((var(--desktop-layout) - var(--responsive-layout-2)) / (var(--mobile-size-1) - var(--desktop-size-1)))
```
1. `desktop-layout` - ширина контейнера на десктопе без единиц измерения (пример: 1600).
2. `responsive-layout-1` - ширина контейнера с единицами измерения, до которого будет происходить сжатие (пример: 320px).
3. `responsive-layout-2` - то же значение, что и в прошлой переменной, но уже без единиц измерения (пример: 320).
4. `desktop-size-1` - размер элемента на десктопе без единиц измерения (пример: 30).
5. `desktop-size-2` - то же значение, что и в прошлой переменной, но уже с единицами измерения (пример: 30px).
6. `mobile-size-1` - конечное значение размера без единиц измерения, до которого нам нужно увеличить элемент (пример: 80).
7. `mobile-size-2` - то же значение, что и в прошлой переменной, но уже с единицами измерения (пример: 80px).

### Пример использования
```
.box {
  /* Отзывчивый font-size */
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
## 🔮 Что важно знать
- В примере используется свойство `font-size`, но это не значит, что данная формула подходит только для данного свойства. Она подходит в целом почти для любого свойства у которого есть размеры.
- В этой формуле вместо пикселей допускаются и другие единицы измерения. Вы можете использовать условно rem, если вам так хочется. Здесь нет никаких ограничений.
- В файле `responsive.css` я подготовил примеры использования данной формулы, а так в целом для работы он не нужен. 
- В файле `responsive.scss` написаны уже готовые миксины. Вот данный файл вы можете подключить к себе в проект и использовать. Это удобно ибо вам не придётся всё это писать вручную.

## 🔱 Создано при поддержке

<a href="https://www.browserstack.com">
  <img src="temp/Browserstack-logo.svg?sanitize=false" width="200" alt="browserstack">
</a> 

## 📃 Что используется в этом репозитории
- Семантическое управление версиями - [semver.org](https://semver.org)
- Соглашение о коммитах - [conventionalcommits.org](https://www.conventionalcommits.org/ru/v1.0.0/)