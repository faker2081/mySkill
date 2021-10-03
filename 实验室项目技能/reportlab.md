# ReportLab

### 常用方法

- Paragraph     文本段落            Paragraph(text,style)

- Spacer          垂直空间留白       Spacer(width, height)

- Table            表格                    Table(data)

- PageBreak    插入分页              PageBreak()

- Image             图片                Image(filename, width=None, height=None)

  ###### 直接使用库提供的文本段落样式:

  ```py
  style=getSampleStyleSheet()
  ```

  - 使用样式如下：

    ```py
    style['title']
    
    # 下面代码查看所有样式及其每个属性的值
    style.list()
    
    #定义样式列表，其中每元组包括样式命令词、样式应用起始单元坐标、样式应用结束单元坐标和样式值。（具体样式命令词请叁阅官方文档）
    style_list =[                            
        ('TEXTCOLOR',(0,0),(1,-1),colors.red),
        ('ALIGN',(0,0),(-1,-1),'CENTER'),
        ('VALIGN',(0,0),(-1,-1),'MIDDLE'),
        ('GRID',(0,0), (-1,-1),1,colors.black),
        ('FONTSIZE',(0,0),(-1,-1),10),
        ('FONT', (0,0), (-1,-1), 'msyh'),
        ('BOTTOMPADDING',(0,0),(-1,-1),2),
        ('TOPPADDING',(0,0),(-1,-1),2)]
    #创建表格样式对象
    mytab_style = TableStyle(style_list)
    #创建表格
    mytable = Table(data_list)
    # 将样式应用到表格
    mytable.setStyle(mytab_style)
    ```

  

