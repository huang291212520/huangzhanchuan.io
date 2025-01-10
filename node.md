从文本中匹配键值对
```javascript
// 匹配如下列键值对
// Select_Service_Area: 'Pilih Kawasan Helpdesk',  
// Area_Malaysia: 'Malaysia',  
// Area_Laos: 'Laos',  
// Area_HongKong: 'Hong Kong',  
// Common_Close: 'Tutup'

// 匹配指定的key
let regx = new RegExp(`(?<=${指定的key}:\n?\\s+?').*(?=')`, 'g')
data.match(regx)[0]

// 匹配所有的key
let allList = readData.match(/[A-Za-z0-1_]+\S:.*(?=\n)/g)  
// 获取最后一个key
let lastItem = allList[allList.length - 1]
// 替换并且新增
let replaceValue = `${lastItem.replace(/,$/, '')},\n${str}`
```

从远程下载资源
```javascript
const https = require('https')  
const http = require('http')

function saveImg(targetUrl, pathUrl) {  
    const protocol = targetUrl.indexOf('https') > -1 ? https : http  
    // 下载远程文件并保存  
    protocol.get(targetUrl, function (response) {  
        const data = []  
        response.on('data', (chunk) => {  
            data.push(chunk)  
        })  
        response.on('error', () => {  
            console.log('图片保存失败！', pathUrl)  
        })  
        response.on('end', () => {  
            console.log('保存成功')  
            const buffer = Buffer.concat(data)  
            fs.writeFileSync(pathUrl, buffer)  
        })  
    })  
}
```