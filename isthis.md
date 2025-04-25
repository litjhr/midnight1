<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>遍历 GitHub 仓库文件</title>
</head>

<body>
    <h1>GitHub 仓库文件列表</h1>
    <ul id="file-list"></ul>

    <script>
        const owner = 'litjhr';
        const repo = 'midnight1';
        const path = '_posts';

        const apiUrl = `https://api.github.com/repos/${owner}/${repo}/contents/${path}`;

        fetch(apiUrl)
          .then(response => {
                if (!response.ok) {
                    throw new Error('网络响应不正常');
                }
                return response.json();
            })
          .then(data => {
                const fileList = document.getElementById('file-list');
                data.forEach(item => {
                    const listItem = document.createElement('li');
                    listItem.textContent = item.name;
                    fileList.appendChild(listItem);
                });
            })
          .catch(error => {
                console.error('发生错误:', error);
            });
    </script>
</body>

</html>
