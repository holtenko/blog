---
title: StarUML 3.0.1 激活教程
toc: true
date: 2018-07-30 21:18:10
categories: [Linux]
tags: [Linux,Wiki]
---

## 安装asar
`npm install -g asar`

## 解压app.asar
进入到`app.asar`目录下执行当前命令。默认文件路径Windows是`C:\Program Files\StarUML\resources`，Mac是`/Applications/StarUML.app/Contents/Resources`。

`asar extract app.asar app`

## 修改激活代码
解压之后当前文件夹下有一个新的目录`app`，真正的验证license的代码在`app\src\engine\license-manager.js`，把的这两个方法替换掉。

```{javascript}
checkLicenseValidity () {
    this.validate().then(() => {
      setStatus(this, true)
    }, () => {
      //setStatus(this, false)
     // UnregisteredDialog.showDialog()
	     setStatus(this, true)
    })
  }
 
  /**
   * Check the license key in server and store it as license.key file in local
   *
   * @param {string} licenseKey
   */
  register (licenseKey) {
    return new Promise((resolve, reject) => {
      $.post(app.config.validation_url, {licenseKey: licenseKey})
        .done(data => {
          var file = path.join(app.getUserPath(), '/license.key')
          fs.writeFileSync(file, JSON.stringify(data, 2))
          licenseInfo = data
          setStatus(this, true)
          resolve(data)
        })
        .fail(err => {
          setStatus(this, true)
          //if (err.status === 499) { /* License key not exists */
           // reject('invalid')
          //} else {
          //  reject()
          //}
        })
    })
  }
  ```

## 重新打包替换原来的app.asar
`asar pack app app.asar`

## 启动StarUML 开始工作吧