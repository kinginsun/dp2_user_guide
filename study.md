### study的基本结构：

```json
{
  "steps": 
[
  {},
  {}
]
}
```

全局变量放在steps同级，只能为简单的 key==>value形式（value为字符串）

steps为一个List结构，每个step按次序放在{}中



##### 下面是一个典型的step的结构：

```json
{

 "project_name": "NMPA_Drug_Law_PageNum",

 "url": "http://www.nmpa.gov.cn/WS04/CL2170/",

 "type": "one-off",

 "priority": 0,

 "fetch_method": "splash",

 "method": "GET",

 "status": 1,

 "charset": "UTF-8",

 "charact_string_start": "药品法规文件",

 "charact_string_end": "国家药品监督管理局",

 "pf_id": 172,

 "lua_id": 90,

 "data_out": {

  "jpath": "{TotalPageNum:TotalPages}"

 }

}
```

##### step结构中支持所有的dp2 task的配置参数，默认的参数如下：

```json
{
    "study_id": None,
    "study_name": None,
    "project_name": None,
    "extra_data": None,
    "url": None,
    "type": "one-off",
    "priority": 0,
    "fetch_method": "direct",
    "method": "GET",
    "data": None,
    "cookies": None,
    "through_proxy": 0,
    "status": 0,
    "charset": "UTF-8",
    "charact_string_start": None,
    "charact_string_end": None,
    "charact_string_notry": None,
    "pf_id": None,
    "ck_id": None,
    "lua_id": None,
}
```

除dp2 task的参数外，step中还含有data_in, data_out两个可选参数，默认是将每个step获得的数据直接传到下一步，若要对传到下一步的数据进行修改，可用data_out来配置；data_in负责对传到这一步的数据进行修饰，然后再转给任务管理程序。

```json
data_out, data_in的结构如下：
{
  "jpath": "",
  "api": {
    "url": "http://dp2.labqr.com/b/dpool/save/data/to/db",
    "table": "drug_law_and_regulation"
    "where": {
      "task_fp": "{task_fp}"
    }
  }
}
```

| First Header | Second Header | Third Header                                                 |
| ------------ | ------------- | ------------------------------------------------------------ |
| jpath        | 可选          | JMESPath查询参数，当值为空时，代表对输入数据不处理           |
| api          | 可选          | 配置数据post到的api地址，包含以下三个参数：url: 必须, table: 可选，设定数据要保存到的表的名称，若API不需要，可以不设定；where: 可选，用来判断数据唯一性的条件，可为一个或多个条件，只能精确匹配；默认为{“id”:”{id}”}, 即用post数据中的id作为唯一性判断的标准。 若用默认的where时，要确保在post data中已经含有id字段 |

![image-20230920114756354](assets/image-20230920114756354.png)
