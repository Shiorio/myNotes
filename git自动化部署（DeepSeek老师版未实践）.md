在前端项目中，通过 Git 实现自动化部署可以借助 CI/CD 工具，以下是一个常见的流程：

### 1. 选择 CI/CD 工具
常用的 CI/CD 工具有：
- **GitHub Actions**（GitHub 自带）
- **GitLab CI/CD**（GitLab 自带）
- **Travis CI**
- **CircleCI**
- **Jenkins**

### 2. 配置 CI/CD 工具
以 **GitHub Actions** 为例：

#### 2.1 创建 GitHub Actions 配置文件
在项目根目录下创建 `.github/workflows/deploy.yml` 文件。

#### 2.2 编写部署脚本
以下是一个简单的 `deploy.yml` 示例：

```yaml
name: Deploy to Production

on:
  push:
    branches:
      - main  # 只在 main 分支推送时触发

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout code
      uses: actions/checkout@v2

    - name: Set up Node.js
      uses: actions/setup-node@v2
      with:
        node-version: '14'

    - name: Install dependencies
      run: npm install

    - name: Build project
      run: npm run build

    - name: Deploy to server
      uses: easingthemes/ssh-deploy@v2.1.5
      with:
        SSH_PRIVATE_KEY: ${{ secrets.SSH_PRIVATE_KEY }}
        SOURCE: "dist/"  # 构建后的目录
        REMOTE_HOST: ${{ secrets.REMOTE_HOST }}
        REMOTE_USER: ${{ secrets.REMOTE_USER }}
        TARGET: /var/www/html  # 服务器目标目录
```

### 3. 配置服务器
确保服务器已安装 SSH 服务，并配置好部署目录的权限。

### 4. 配置 GitHub Secrets
在 GitHub 仓库的 `Settings -> Secrets` 中添加以下密钥：
- `SSH_PRIVATE_KEY`：SSH 私钥
- `REMOTE_HOST`：服务器 IP 或域名
- `REMOTE_USER`：服务器用户名

### 5. 推送代码
将代码推送到 `main` 分支，GitHub Actions 会自动执行部署流程。

### 6. 验证部署
访问服务器，确认部署是否成功。

### 其他 CI/CD 工具
其他工具的配置类似，只需在对应平台创建配置文件并设置触发条件即可。

### 总结
通过 Git 和 CI/CD 工具，前端项目可以实现自动化部署，提升效率并减少人为错误。