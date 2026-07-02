# GitHub Pages 部署步骤

下面是最省事的部署方式，适合把这个展示页挂到简历或套磁邮件里。

## 方式一：新建独立仓库

1. 在 GitHub 新建仓库，例如：

```text
paper-kg-showcase
```

2. 把 `paper_kg_showcase` 里的文件放到仓库根目录。

3. 提交并推送：

```powershell
git init
git add .
git commit -m "Add paper KG showcase"
git branch -M main
git remote add origin https://github.com/<your-name>/paper-kg-showcase.git
git push -u origin main
```

4. 打开 GitHub 仓库：

```text
Settings -> Pages -> Build and deployment
```

选择：

```text
Source: Deploy from a branch
Branch: main
Folder: /root
```

5. 等待 Pages 构建完成，访问：

```text
https://<your-name>.github.io/paper-kg-showcase/
```

## 方式二：放到个人主页仓库

如果你已经有 `<your-name>.github.io` 仓库，可以把这个目录作为子目录：

```text
paper-kg/
```

访问地址会类似：

```text
https://<your-name>.github.io/paper-kg/
```

## 简历里怎么放链接

建议放在科研经历对应项目后面：

```text
项目展示页：github.io/xxx/paper-kg-showcase
```

如果担心链接太长，可以用 GitHub Pages 原链接，不建议使用短链。

## 公开前检查

- `assets/graph_data.js` 只包含抽样演示数据。
- 页面中没有本地绝对路径。
- 页面中没有账号、密码、数据库连接字符串。
- README 中没有课题组未公开材料。
- 原始大数据、Neo4j 数据库文件、投稿论文材料不要放进公开仓库。
