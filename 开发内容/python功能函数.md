# python 功能函数

## 文件内容写入

```python
def writdoc(name,doc):
    # 打开「detail_content」文件
    fout = open(name, 'w', encoding='utf8')
    # 写入文件内容
    fout.write(doc)
    #关闭文件
    fout.close()
```

