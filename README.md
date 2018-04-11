# router-demo

[hash实现路由切换](https://github.com/clydeqin7/router-demo/blob/735761d590e58cafd23c48ce10e7f7f85a3d96b0/index.html)

通过`hash`和`onhashchage` 实现切换路由，还可以将如`www.xxx.com#0`url进行分享

```css
    <x-tab>
        <ol class="nav">
            <li><a href="#0">tab1</a></li>
            <li><a href="#1">tab2</a></li>
        </ol>
        <ol class="content">
            <li>content1</li>
            <li>content2</li>
        </ol>
    </x-tab>
```

```javascript
    selectTab()
    window.onhashchange = function(){
        selectTab()
    }
    function selectTab(){
        let index = location.hash || '#0' //默认高亮第0个
        index = index.substring(1)
        $('x-tab > .nav > li').eq(index).addClass('active')
            .siblings().removeClass('active')
        $('x-tab > .content > li').eq(index).addClass('active')
            .siblings().removeClass('active')       
    }
```

[History API实现路由切换](https://github.com/clydeqin7/router-demo/blob/e6ad4dd1b6dc0e51836227ea97df9b1728de54c5/index.html)

通过 ```window.history.pushState```进行了路由切换，此时将如`www.xxx.com/tab1`的URL进行分享会有问题，还需要服务器对这个路劲进行处理。

```css
    <x-tab>
        <ol class="nav">
            <li><a href="./tab1">tab1</a></li>
            <li><a href="./tab2">tab2</a></li>
        </ol>
        <ol class="content">
            <li>content1</li>
            <li>content2</li>
        </ol>
    </x-tab>
    <a href="#top">回到顶部</a>
```

```javascript
selectTab()
    $('x-tab').on('click', ' .nav > li > a', (e)=>{
        e.preventDefault()
        let a = e.currentTarget
        let path = a.getAttribute('href')
        window.history.pushState({}, 'xxx', path)
        selectTab()
    })
    function selectTab(){
        let index = location.pathname.substring(1) || 'tab1' //默认tab1
        index = index.substring(3)
        $('x-tab > .nav > li').eq(index - 1).addClass('active')
            .siblings().removeClass('active')
        $('x-tab > .content > li').eq(index - 1).addClass('active')
            .siblings().removeClass('active')       
    }
```

