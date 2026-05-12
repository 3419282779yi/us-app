# 「我们之间」部署指南

你的小程序已完成，在 `D:\Desktop\us-app\index.html`。

## 你现在要做的（3 件事）

### 1. 注册 Supabase（2 分钟）

1. 打开 https://supabase.com，点 Sign In，用 GitHub 账号登录
2. 点 New project，填写:
   - Name: us-app
   - Password: 设置一个密码并记下来
   - Region: Northeast Asia (Tokyo)
3. 点 Create project，等 1-2 分钟

### 2. 建表（30 秒）

左侧菜单 → SQL Editor → New query，粘贴以下 SQL 并点击 Run:

```sql
DROP TABLE IF EXISTS couples;
CREATE TABLE couples (
  id SERIAL PRIMARY KEY,
  pair_code TEXT UNIQUE NOT NULL,
  data JSONB DEFAULT '{}',
  updated_at TIMESTAMPTZ DEFAULT NOW()
);
ALTER TABLE couples ENABLE ROW LEVEL SECURITY;
CREATE POLICY "all_access" ON couples FOR ALL USING (true);
```

### 3. 获取连接信息

左侧 Settings → API:
- 复制 Project URL (格式: https://xxxxx.supabase.co)
- 复制 anon public key

---

## 使用

1. 手机打开 index.html
2. 首次打开会提示输入配对码，你俩输入相同的配对码
3. 点击"配置 Supabase"，填入上一步的 URL 和 Key
4. 完成！两个人就能实时同步数据了

---

## 部署到公网（可选）

如果想让女朋友直接通过链接访问，不用传文件:

### 方案 A: GitHub Pages（推荐，永久免费）

1. 去 github.com 创建一个新仓库，名字随意（如 us-app）
2. 在本机执行:

```bash
cd D:\Desktop\us-app
git remote add origin https://github.com/你的用户名/us-app.git
git push -u origin master
```

3. 在 GitHub 仓库页面 → Settings → Pages:
   - Source: Deploy from a branch
   - Branch: master, / (root)
   - 点 Save

4. 几分钟后，链接就是: https://你的用户名.github.io/us-app/

### 方案 B: Surge（最快，一命令）

```bash
npx surge D:\Desktop\us-app
```

按提示注册（邮箱+密码），会得到一个 https://xxx.surge.sh 的永久链接。
