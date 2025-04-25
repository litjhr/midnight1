---
layout: page
title: Welcome to my blog!
---

<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>遍历 GitHub 仓库文件及链接</title>
    <style>
        #loading {
            display: none;
        }
    </style>
</head>

<body>
    <h1>GitHub 仓库文件列表及链接</h1>
    <div id="loading" >正在加载...&gt~&lt</div>
    <ul id="file-list"></ul>
    <script>
        const owner = 'litjhr';
        const repo = 'midnight1';
        const path = '_posts';
        const apiUrl = `https://api.github.com/repos/${owner}/${repo}/contents/${path}`;
        const loadingElement = document.getElementById('loading');
        const fileList = document.getElementById('file-list');
        // 显示加载提示
        loadingElement.style.display = 'block';
        fetch(apiUrl)
          .then(response => {
                if (!response.ok) {
                    throw new Error('网络响应不正常');
                }
                return response.json();
            })
          .then(data => {
                // 隐藏加载提示
                loadingElement.style.display = 'none';
                data.forEach(item => {
                    const listItem = document.createElement('li');
                    const link = document.createElement('a');
                    link.href = item.html_url;
                    link.textContent = item.name;
                    listItem.appendChild(link);
                    fileList.appendChild(listItem);
                });
            })
          .catch(error => {
                // 隐藏加载提示
                loadingElement.style.display = 'none';
                console.error('发生错误:', error);
            });
    </script>
</body>

</html>  
