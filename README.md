# 🌾 农业数据管理系统

一个基于 Flask + SQLAlchemy + 前端的农业数据可视化管理系统，支持省份农业数据、传感器数据、价格销量管理。


## 📊 功能特性

### 前端功能

#### 管理页面 (admin.html)
- ✅ 省份农业数据管理
- ✅ 传感器数据管理
- ✅ 价格销量管理
- ✅ 作物类型管理
- ✅ 数据库连接配置
- ✅ 存储模式切换 (localStorage/MySQL)
- ✅ 数据验证和范围检查
- ✅ 实时时间显示

#### 可视化页面 (front.html)
- ✅ 农业数据可视化
- ✅ 中国地图展示
- ✅ 多维度数据图表

## 🗄️ 数据库结构

### crop 表 (作物数据)
```sql
CREATE TABLE crop (
    type VARCHAR(20) PRIMARY KEY COMMENT '作物类型',
    day INT COMMENT '成熟天数',
    output DECIMAL(10,2) COMMENT '产量',
    price DECIMAL(10,2) COMMENT '售价'
);
```

### weather 表 (天气/传感器数据)
```sql
CREATE TABLE weather (
    date DATE PRIMARY KEY COMMENT '日期',
    temp DECIMAL(10,2) COMMENT '温度',
    wet DECIMAL(10,2) COMMENT '湿度',
    sun DECIMAL(10,2) COMMENT '日照',
    tsoil1 DECIMAL(10,2) COMMENT '土壤第一层',
    tsoil2 DECIMAL(10,2) COMMENT '土壤第二层',
    tsoil3 DECIMAL(10,2) COMMENT '土壤第三层'
);
```

### area 表 (地区粮食产量数据)
```sql
CREATE TABLE IF NOT EXISTS area (
  prov   VARCHAR(20)   NOT NULL,
  type   VARCHAR(20)   NULL,
  output DECIMAL(10,2) NULL,
  PRIMARY KEY (prov)
);
```

### user 表 (用户信息表)
```sql
CREATE TABLE IF NOT EXISTS user (
  uid      INT AUTO_INCREMENT,
  username VARCHAR(20) NOT NULL,
  password VARCHAR(20) NOT NULL,
  anth     INT         NOT NULL,
  PRIMARY KEY (uid),
  UNIQUE KEY uk_username (username)
);
```

## 🔧 配置说明

### 前端配置 (admin.html)

数据库连接配置：
```javascript
const DB_CONFIG = {
    storageMode: 'localStorage',  // 'localStorage' 或 'database'
    database: {
        type: 'mysql',
        host: 'localhost',
        port: 3306,
        name: 'myollama',
        user: 'root',
        password: ''
    },
    apiBaseUrl: 'http://localhost:3000/api'
};
```

## 🐛 故障排除

### 1. 数据库连接失败
- 检查MySQL服务是否启动
- 验证数据库连接参数是否正确
- 确认数据库和表是否已创建

### 2. 前端无法访问后端
- 确认后端服务是否启动 (http://localhost:3000)
- 检查浏览器控制台是否有CORS错误
- 验证API地址配置是否正确

**AgriSage农业数据管理系统** - 让农业数据管理更简单、更智能 🌾 
