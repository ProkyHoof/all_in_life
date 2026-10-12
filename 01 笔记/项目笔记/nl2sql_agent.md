---
tags:
  - 项目
类型: Agent
状态: 构思中
开始日期: 2026-10-12
截止日期:
关联知识:
关联资源:
---

# 1 README  


# 1 day 01  
## 1.1 确认 Git 推送成功  

``` bash
git add .
git commit -m "chore: 初始化项目结构"
git branch -M main
git remote add origin https://github.com/你的用户名/nl2sql-agent.git
git push -u origin main
```

## 1.2 安装依赖  

``` bash
pip install openai pydantic sqlalchemy fastapi "uvicorn[standard]" python-dotenv
pip freeze > requirements.txt
```

