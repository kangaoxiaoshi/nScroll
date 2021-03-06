# mScroll -- pull down refresh and pull up load more. only use in Mobile devices

[![NPM](https://nodei.co/npm/mscroll.png?downloads=true&downloadRank=true&stars=true)](https://nodei.co/npm/mscroll/)<br/>
1. pull down update
1. pull up load more

#use document
## online demo <font color=#ab1761  face="黑体">(only work in mobile devices)</font>
  https://kangaoxiaoshi.github.io/mscroll/
## install
```
  npm install mscroll --save
```
## useage
```
1. npm run build

1. browserify mscroll.js --deubg > bundle.js

1. in browser use bundle.js
```
##dependency
```
zepto-modules
```
## API
###
.pull
```js
  var Pull = mScroll.pull;
  var refresh = new Pull ('.js-content', {
    msgElement: '.js-msgwrap',
    msgs: ['下拉刷新.....', '释放刷新'],
    distance: 10,
    start: function () {
      //console.info('start');
    },
    move: function () {
      //console.info('move');
    },
    end: function () {
      //console.info('end');
    },
    onRefresh: function () {
      let ul = document.querySelector('.js-ul');                    
      let random = 1; 
      // after refresh do something you want
      setTimeout(() => {           
        this.backTop();
        ul.innerHTML = '';
        for (let i = 0; i< 25; i++) {
          random = (Math.random() * (20 - 1) + 1).toFixed(0);
          ul.innerHTML +=`<li>
                          我是刷新后内容${random}
                         </li>`;
        }
      }, 1000);
    }
  });
```
  *  {msgElement} ``required``  selector or  document.element  where to place the refresh state message.
  *  {msgs}  default ['下拉刷新.....', '释放刷新'] when pulling  display msg.
  *  {distance} default 40px msgElement  height.
  *  {start} ``function`` when start pull fire this function.
  *  {move} ``function`` when  pulling fire this function.
  *  {end} ``function`` when  finish pull fire this function.
  *  {onRefresh} ``function`` after pull  do what you want in this function.

.more
```js
  var More = mScroll.more;
  var load = new More ('.js-content', {
    main: '.js-content',        
    more: function () {
      //load more function
      console.log('load more');
    }
  });
```
  *  {.js-content} ``required`` part of ``main`` this.el is $('.js-content').
```js
  this.$main.off('scroll').on('scroll', _.throttle((e) => {
    if (this.el && this.el.getBoundingClientRect().bottom < document.body.clientHeight + 25) {        
      this.$el.trigger('load-bottom');        
    }
  }, 200));
```
  *  {main} ``required`` selector or  document.element  which to add scroll.


