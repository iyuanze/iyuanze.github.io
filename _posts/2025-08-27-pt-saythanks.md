---
layout: mypost
title:  某齐PT站自动“说谢谢”自动脚本获取魔力
categories: [PT,说谢谢,自动,脚本]
---

获得了一个某齐PT站的邀请，主要是以图书为主的PT站，印象里面这个站点开通不是很久，用户增长的还是比较快。
目前有2300+用户，种子数1800+，种子总容量5T+，网站用的是NexusPHP框架。

目前已经是需要通过邀请才能进入了，并且设置了新手考核：</br>
名称：新手考核</br>
时间：2025-08-22 09:14:04 ~ 2025-09-21 09:14:04</br>
指标1：上传增量, 要求：20 GB, 当前：28.02 GB, 结果：通过！</br>
指标2：下载增量, 要求：20 GB, 当前：0.00 KB, 结果：未通过！</br>
指标3：魔力增量, 要求：10000 , 当前：2557, 结果：未通过！</br>

因为用R4S做软路由，挂了Qbittorrent,下载几个热门种子，获取上传还是不难。下载的话晚两天找个非free的种子下载一下就能达成。
对于魔力增量，就需要大量的保种获得时魔，在加上每日签到才能达成了。

研究发现网站有个魔力增加机制，是通过对发布种子的链接，对该种子发布者点击“说谢谢”按钮，鼓励发布者的同时，自己可以获得10魔力。
所以，在获得时魔和每天签到之外，可以多点击“说谢谢”获得魔力。这个也可以通过在浏览器控制台运行javascript来实现。

前期准备：</br>
1，chrome或者edge浏览器（我用的edge）</br>
2，进入“全部种子”的菜单/torrents.php（注意：需要手动翻页，大概每页100个种子）</br>
3，给浏览器设置对本网站允许弹出窗口</br>
- 在计算机上打开 Chrome。
- 在右上角，依次点击“更多”图标 展开 接着点按 设置。
- 依次点击隐私设置和安全性 接着点按 网站设置 接着点按 弹出式窗口和重定向。
- 允许发送弹出式窗口并使用重定向
- 添加你允许弹出窗口的网站（就是你准备操作的PT站）</br>

4，在需要操作的网页点击右键“检查”，或者按F12，打开开发者工具</br>
5，在控制台中输入javascript代码，回车运行（如果之前没有使用过，需要先输入“允许粘贴”回车）</br>

代码内容：


```javascript
// 获取所有标题列的链接
const titleLinks = Array.from(document.querySelectorAll('table.torrents a[href^="details.php?id="]'))
  .map(a => a.href)
  .filter(href => href.includes('details.php'));

// 如果没有找到链接，则退出
if (titleLinks.length === 0) {
  console.log('未找到符合条件的链接');
}

let currentIndex = 0;

// 处理单个链接的函数
function processLink(url) {
  return new Promise((resolve, reject) => {
    // 在新窗口中打开链接
    const newWindow = window.open(url, '_blank');
    
    if (!newWindow) {
      reject(new Error('弹出窗口被阻止，请允许弹出窗口'));
      return;
    }
    
    // 等待新窗口加载完成
    newWindow.addEventListener('load', function() {
      try {
        // 查找并点击"说谢谢"按钮
        const thanksButton = newWindow.document.getElementById('saythanks');
        
        if (thanksButton) {
          thanksButton.click();
          console.log(`已点击链接 ${currentIndex + 1}/${titleLinks.length} 的"说谢谢"按钮`);
          
          // 等待短暂时间确保点击生效，然后关闭窗口
          setTimeout(() => {
            newWindow.close();
            resolve();
          }, 1000);
        } else {
          newWindow.close();
          reject(new Error('未找到"说谢谢"按钮'));
        }
      } catch (error) {
        newWindow.close();
        reject(error);
      }
    });
    
    // 设置超时处理
    setTimeout(() => {
      if (newWindow && !newWindow.closed) {
        newWindow.close();
        reject(new Error('页面加载超时'));
      }
    }, 10000); // 10秒超时
  });
}

// 依次处理所有链接的主函数
async function processAllLinks() {
  for (currentIndex = 0; currentIndex < titleLinks.length; currentIndex++) {
    try {
      console.log(`正在处理第 ${currentIndex + 1} 个链接: ${titleLinks[currentIndex]}`);
      await processLink(titleLinks[currentIndex]);
      
      // 在链接之间添加短暂延迟，避免过快请求
      if (currentIndex < titleLinks.length - 1) {
        await new Promise(resolve => setTimeout(resolve, 2000));
      }
    } catch (error) {
      console.error(`处理链接 ${titleLinks[currentIndex]} 时出错:`, error.message);
    }
  }
  
  console.log('所有链接处理完成');
}

// 开始处理
processAllLinks();
