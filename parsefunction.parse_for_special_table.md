**按列标题提取表格数据（列数固定，行数可变）**

```json
{
  "elements": {
    "table": {
      "rows": "//div[@class='monograph_details_text_content']",
      "cells": "./label|./div",
      "title_column": {
        "fields": {
          "dp2_id": {
            "col": "TASK_id"
          },
          "standard_InChI": {
            "col": ".//div[@id='InCHI_val']",
            "name": "Standard InChI:"
          },
          "standard_InChIKey": {
            "col": ".//div[@id='inchikey_val']",
            "name": "Standard InChIKey:"
          }
        }
      }
    }
  },
  "data_out": "merge(table,additional_properties)"
}
```

1. 配置放在elements的一个字段中
2. rows是表格中每一行的路径
3. cells指定每一行中要提取的单元格的相对路径，若有多种时，用"|"分别写出来
4. title_column设置每一个字段的要匹配的行名字name，col设定内容所在的相对路径
5. title_column中也可以设定title所在列的序号title_index（默认0），以及content中所在列的序号content_index（默认1）
6. 每个字段中的col可以设定为相当于内容单元格的相对路径，以”./“开头；若不是”./“开头，则认为是全局的路径
7. fields中的字段，可以通过name确定row_index，也可以直接指定row_index

**按第一行标题提取表格数据（列数不固定，行数可变）**

```json
{
  "elements": {
    "list": {
      "rows": "//table[@class='']//tr",
      "cells":"./td",
      "title_row": "//table[@class='td1']//tr/td",
    }
  }
}

{
  "elements": {
    "list": {
      "rows": "//table[@class='']//tr",
      "cells":"./td",
      "title_row": {
        "col": "//table[@class='td1']//tr/td",
        "fields":{
          "sn":{
            "name":"流水号"
          },
          "general_name":{
            "col":".",
            "name":"通用名",
            "col_index":2
          }
        }
      }
    }
  }
}
```

1. 配置放在elements的一个字段中
2. rows是表格中每一行的路径（不包含标题所在的行，仅是内容的行）
3. cells指定内容中每一行中要提取的单元格的相对路径（默认为“./td”），若有多种时，用"|"分别写出来
4. title_row为字串时，即为标题行所在的路径，默认用标题中文字作为每个字段的名字
5. title_row为dict时，col指定标题行路径（要指定到具体标题名字的位置），fields指定每个字段的名字和相对路径，默认为”."
6. fields中的设置方法与前相同，name指定标题的名字，需完全匹配，col指定相对路径, col_index指定时，则用这个序号，忽略name; 若无col_index时，根据name确定col_index