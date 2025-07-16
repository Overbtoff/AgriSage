# 🌾 农业数据管理系统

一个基于 Flask + SQLAlchemy + 前端的农业数据可视化管理系统，支持省份农业数据、传感器数据、价格销量管理。

## 🚀 快速开始

### 1. 环境要求

- Python 3.7+
- MySQL 5.7+
- 现代浏览器 (Chrome, Firefox, Safari, Edge)

### 2. 安装依赖

```bash
# 安装Python依赖包
pip install -r requirements.txt
```

### 3. 配置数据库

1. 启动MySQL服务
2. 创建数据库：
```sql
CREATE DATABASE myollama CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
```

3. 修改 `server.py` 中的数据库连接参数：
```python
USERNAME = 'root'           # 数据库用户名
PASSWORD = '123456'         # 数据库密码
HOSTNAME = 'localhost'      # 数据库主机
PORT = 3306                 # 数据库端口
DATABASE = 'myollama'       # 数据库名称
```

### 4. 启动服务

#### Windows用户
双击运行 `start_server.bat`

#### 其他系统用户
```bash
python start_server.py
```

### 5. 访问系统

- 后端API: http://localhost:3000
- 前端管理页面: http://localhost:5500/admin.html
- 前端可视化页面: http://localhost:5500/front.html

## 📊 功能特性

### 后端API (Flask + SQLAlchemy)

#### 数据库连接测试
- `POST /api/db/test-mysql` - 测试MySQL连接

#### 作物数据管理
- `GET /api/crop` - 获取所有作物数据
- `POST /api/crop` - 添加作物数据
- `PUT /api/crop/<type>` - 更新作物数据
- `DELETE /api/crop/<type>` - 删除作物数据

#### 天气/传感器数据管理
- `GET /api/weather` - 获取所有天气数据
- `GET /api/weather?date=2024-01-01` - 获取指定日期天气数据
- `POST /api/weather` - 添加天气数据
- `PUT /api/weather/<date>` - 更新天气数据
- `DELETE /api/weather/<date>` - 删除天气数据

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

### 后端配置 (server.py)

数据库连接：
```python
USERNAME = 'root'
PASSWORD = '123456'
HOSTNAME = 'localhost'
PORT = 3306
DATABASE = 'myollama'
```

## 📝 使用说明

### 1. 数据库模式
- 在管理页面右上角可以切换存储模式
- localStorage模式：数据存储在浏览器本地
- database模式：数据存储在MySQL数据库

### 2. 数据验证
系统内置了完善的数据验证规则：
- 产量范围验证（根据省份和作物类型）
- 传感器数据范围验证
- 价格销量数据验证
- 收成天数验证

### 3. 作物类型管理
- 支持自定义添加作物类型
- 作物类型会同步到下拉选择框

## 🐛 故障排除

### 1. 数据库连接失败
- 检查MySQL服务是否启动
- 验证数据库连接参数是否正确
- 确认数据库和表是否已创建

### 2. 前端无法访问后端
- 确认后端服务是否启动 (http://localhost:3000)
- 检查浏览器控制台是否有CORS错误
- 验证API地址配置是否正确

### 3. 依赖包安装失败
```bash
# 升级pip
python -m pip install --upgrade pip

# 重新安装依赖
pip install -r requirements.txt --force-reinstall
```

## 📄 许可证

MIT License

## 🤝 贡献

欢迎提交Issue和Pull Request！

---

**农业数据管理系统** - 让农业数据管理更简单、更智能 🌾 