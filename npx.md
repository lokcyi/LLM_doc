# npm vs npx 
Npm(node package manger) 是套件管理工具，\
讓你在開發過程中，可以把想要的 node 套件，透過 npm 安裝在 local 專案位置或是 global 全局性整台電腦的環境下面。\
這就是 npx 用處所在了。 \
npx 是在 npm v5.2.0 之後內建的指令，也是一種 CLI 工具，讓我們可以更方便的安裝或是管理依賴(dependencies)，就來看看 npx 可以怎麼幫助我們，以及和 npm 主要的差異在哪裡。
- npm 永久安裝，npx 安裝後即移除
> 我要建立一個 Nuxt.js App \
> 以 npm 的方式建立：
```console
$ npm install -g create-nuxt-app // 安裝一個叫 create-nuxt-app 的套件
$ create-nuxt-app my-nuxt-app    // 使用這個套件初始一個nuxt app起來
```
> 以 npx 的方式建立：
```console
$ npx create-nuxt-app my-nuxt-app
```
npm 會全局性的安裝 create-nuxt-app，這個 dependency 也會一直存在在你的本機 node_modules 下，\
如果使用 npx 命令，他會安裝在臨時安裝包上，等到項目初始化完成後就刪除，不用全局性的安裝，避免被汙染
