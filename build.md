```
优化打包配置和首页加载速度
1、路由按需加载
2、开启gzip压缩
3、momoent.js语言包去除
4、去除预加载prefetch
5、外部文件引入，抽离模块 ( externals )
6、去除sourceMap 
```

## v3 多入口配置

#### 启动命令
```
``` javascript
启动命令传入参数：vite --mode params
```

#### 模板文件
``` html
<script type="module" src="/@vite-env-ENTRY_FILE"></script>
```

#### vite.config
``` javascript
export default defineConfig(({ mode }) => {  
    const entryFile = mode === 'winbox' ? '/src/entryA.ts' : '/src/entryB.ts'  
    return {  
        plugins: [  
            {  
                name: 'html-transform',  
                transformIndexHtml(html) {  
                    console.log(html, 'html')  
                    return html.replace('/@vite-env-ENTRY_FILE', entryFile)  
                },  
                transform(code, id) {  
                    if (id.endsWith('.html')) {  
                        return code.replace('/@vite-env-ENTRY_FILE', entryFile)  
                    }  
                    return code  
                }  
            }  
        ],  
    }  
})

```
