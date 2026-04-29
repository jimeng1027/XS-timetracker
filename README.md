# ⏱ Trello Time Tracker Power-Up

## 功能说明

| 功能 | 描述 |
|------|------|
| 卡片打卡按钮 | 在任意 Trello 卡片内弹出打卡 UI |
| 多人独立打卡 | 不同人输入姓名，各自 clock in/out |
| 实时计时 | 显示本次打卡时长 |
| 卡片徽章 | 卡片上显示打卡状态/今日工时 |
| 工时报表 | 按人员、按项目、明细三维度查询 |
| 日期筛选 | 支持自定义时间段查询总工时 |

---

## 部署步骤

### 1. 托管文件

将以下三个文件上传到任意支持静态网页的服务（推荐免费方案）：

- **GitHub Pages**（推荐）：创建公开仓库 → 上传文件 → 开启 Pages
- **Netlify**：拖拽文件夹即可部署
- **Vercel**：同上

```
上传这三个文件：
├── index.html        ← Power-Up 入口
├── card-button.html  ← 打卡弹窗
└── reports.html      ← 工时报表弹窗
```

假设部署后网址为：`https://your-domain.com/timetracker/`

---

### 2. 在 Trello 创建 Power-Up

1. 访问 https://trello.com/power-ups/admin
2. 点击 **New** 创建新 Power-Up
3. 填写：
   - **Name**: Time Tracker
   - **Iframe connector URL**: `https://your-domain.com/timetracker/index.html`
   - **Capabilities** 勾选：
     - ✅ `card-buttons`
     - ✅ `card-badges`
     - ✅ `board-buttons`
4. 保存

---

### 3. 在看板启用

1. 打开你的 Trello 看板
2. 右上角菜单 → **Power-Ups**
3. 搜索你创建的 "Time Tracker"
4. 点击 **启用**

---

## 使用方法

### 打卡
1. 点开任意 Trello 卡片
2. 右侧点击 **⏱ 打卡记录** 按钮
3. 输入你的姓名（会自动记住）
4. 点击 **▶ 开始打卡**
5. 完成后点击 **■ 结束打卡**

### 查看工时报表
- 点击看板顶部的 **📊 工时报表** 按钮
- 选择日期范围 + 人员/项目筛选
- 点击查询，支持三种视图：
  - **按人员**：每人总工时汇总
  - **按项目**：每张卡片（项目）工时汇总
  - **明细**：所有打卡记录列表

---

## 数据说明

- 数据存储在 Trello 看板的 `shared` storage 中
- 同一看板的所有 Power-Up 用户共享数据
- 自动保留最近 **30 天**记录
- 每条记录包含：姓名、卡片名称、打卡/结束时间

---

## 注意事项

- Trello Power-Up 需要部署在 **HTTPS** 的域名下
- 如本地测试，可使用 `npx serve .` + ngrok 做临时 HTTPS 隧道
- 数据储存上限约 4KB，30天自动清理可保证正常运行
