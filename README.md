# 一、Overview
## 1-1、安裝
```
$ pip install fastapi
$ pip install uvicorn[standard]
```
## 1-2、基本架構
```python
"""
程式名稱： main.py
"""
# 從 fastapi 載入 FastAPI 物件
from fastapi import FastAPI

# 創建 FastAPI 實例
app = FastAPI()

# 設置操作路徑（裝飾器），常用的有 @app.get、@app.post、@app.put、@app.delete
@app.get('/')                               
def root():
    # 函數返回值，可以是 list、dict、str、int、或是 Pydantic 物件...
    return {"message": "Hello World"}
```
## 1-3、啟動
### A. 於命令列呼叫
```
$ uvicorn main.app --reload
```
### B. 於檔案中呼叫
```python
from fastapi import FastAPI
import uvicorn

app = FastAPI()
@app.get('/')
def root():
    return {'message':'Hello World'}

if __name__ == '__main__':
    uvicorn.run(app, host='0.0.0.0', port=8000)
    # 如果要設置更新後自動重啟，則 1st 參數必須為字串
    # uvicorn.run('main:app', host='0.0.0.0', port=8000, reload=True)
```

# 二、路徑（route）操作裝飾器中的路徑參數
## 2-1、可於路徑裝飾器中設置動態參數，並於函數參數指明型別，若不指明則預設為字串型別
```python
@app.get('/items/{item_id})
def read_item(item_id: int):                    # 預設為字串型別
    return {'item_id': item_id}
```
- 型別常用的有 int, str, float, bool，或是更複雜的類型
- 當指定了型別，FastAPI 會針對輸入的資料作型別檢驗
- 若沒有指定型別，則所有的輸入將都會視為字串型別
## 2-2、可以使用 enum 來限定資輸入資料的有效值
```python
from enum import Enum
from fastapi import FastAPI

class Class_Student(str, Enum):
    Name = 'John Doe'
    Year = 18
    Id = '202110001'
    student = True

app = FastAPI()

@app.get('/student/{attr}')
def read_student_info(attr: Class_Student):
    return {'name': attr.Name}
```
## 2-3、路徑參數也可以是路徑值（file path）
- 例如：http://localhost:8000/files/$/$home/john/data.txt $\Rightarrow$ 會得到路徑 /home/john/data.txt
  - 注意：home 之前有二條 /，第二個 / 表為從根目錄起…
```pthon
@app.get('/files/{file_path:path})
def read_file(path):
    return {'file_path': file_path}
```

# 三、查詢參數

# 四、請求體（Request Body）

# 五、設置查詢參數的驗證條件（字串驗證）

# 六、設置路徑參數的驗證條件（數值驗證）

# 七、請求體多種參數

# 八、Body-Schema 模型

# 九、Body-Nested Models 嵌套模型

# 十、Extra Data Types 額外數據類型s

# 十一、Cookie Parameters

# 十二、Header Parameters

# 十三、響應模型（Response Model）
