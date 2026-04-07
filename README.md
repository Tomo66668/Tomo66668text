# 爱图表企业版落地页

这是一个纯静态落地页项目，不依赖 Node.js、npm、构建工具或运行时服务。

## 项目类型

- 纯静态 HTML 项目
- 入口文件：`index.html`
- 样式文件：`styles.css`
- 静态资源：`logo.png`

## 本地运行

直接打开 `index.html` 即可预览，但更推荐使用静态服务器，避免相对路径和缓存问题。

### 方式一：Python

```bash
cd /Users/apple/Oscartext
python3 -m http.server 4173
```

打开：`http://127.0.0.1:4173`

### 方式二：Node.js（可选）

如果你本机已安装 Node.js，也可以直接使用：

```bash
cd /Users/apple/Oscartext
npx serve .
```

## 安装命令

本项目本身无需安装依赖。

```bash
git clone https://github.com/oscartan51400/Oscartext.git
cd Oscartext
```

## 启动命令

```bash
python3 -m http.server 4173
```

## 构建命令

本项目无需构建，没有 `build` 步骤。

## 环境变量

本项目不需要环境变量。

唯一需要注意的是页面引用了 Google Fonts：

- `https://fonts.googleapis.com`
- `https://fonts.gstatic.com`

如果部署环境无法访问 Google Fonts，页面仍可打开，但字体会回退为系统字体。

## 部署方案

### 1. GitHub Pages

最省事，适合这个项目。

如果仓库根目录已经是静态文件结构，只需：

1. 进入 GitHub 仓库 `Settings`
2. 打开 `Pages`
3. `Source` 选择 `Deploy from a branch`
4. Branch 选择 `main`
5. Folder 选择 `/ (root)`
6. 保存后等待 GitHub 发布

如果要用命令行推送：

```bash
git add .
git commit -m "docs: improve deployment guide"
git push origin main
```

### 2. Netlify

适合零配置部署。

在 Netlify 中创建新站点后填写：

- Build command：留空
- Publish directory：`.`

也可以使用 Netlify CLI：

```bash
npm i -g netlify-cli
cd /Users/apple/Oscartext
netlify deploy
netlify deploy --prod
```

### 3. Vercel

同样可以直接托管静态站点。

在 Vercel 中导入仓库后填写：

- Framework Preset：`Other`
- Build Command：留空
- Output Directory：`.`

CLI 方式：

```bash
npm i -g vercel
cd /Users/apple/Oscartext
vercel
vercel --prod
```

### 4. Nginx

适合部署到自己的服务器。

把项目文件上传到站点目录，例如：

```bash
sudo mkdir -p /var/www/oscartext
sudo cp -R /Users/apple/Oscartext/* /var/www/oscartext/
```

示例 Nginx 配置：

```nginx
server {
    listen 80;
    server_name your-domain.com;

    root /var/www/oscartext;
    index index.html;

    location / {
        try_files $uri $uri/ /index.html;
    }
}
```

重载配置：

```bash
sudo nginx -t
sudo systemctl reload nginx
```

## 已验证结果

- 仓库可以正常拉取
- 项目可以通过静态服务器正常访问
- 本地预览返回 `200 OK`
- 项目不需要安装依赖、不需要构建、不需要环境变量
