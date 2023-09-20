```json
{
  "STU": "company.tfyy.drugs",
  "excluded_workers": [],
  "steps": [
    {
      "data_in": {
        "data_for_test": [
          {
            "note": ""
          }
        ]
      },
      "project_name": "{STU}.totalpage",
      "url": "http://www.topfond.com/product/25/",
      "type": "one-off",
      "priority": 2,
      "fetch_method": "direct",
      "method": "GET",
      "status": 1,
      "charset": "UTF-8",
      "charact_string_start": "",
      "charact_string_end": "",
      "pf_id": 1682,
      "data_out": [
        {
          "jpath": "{TotalPageNum:TotalPageNum}"
        }
      ],
      "interval": 86400,
      "excluded_workers": "{excluded_workers}"
    },
    {
      "data_in": {
        "data_for_test": {
          "TotalPageNum": "1"
        }
      },
      "project_name": "{STU}.list",
      "url": {
        "pattern": "http://www.topfond.com/comp/portalResProduct/list.do?compId=portalResProduct_list-15935150754688592&orderType=0&orderColumn=def&productCateId=5&pageSize=6&currentPage=(*)",
        "iteration": {
          "start": 1,
          "stops": "1",
          "stop": "{TotalPageNum}",
          "format": "{}"
        }
      },
      "type": "one-off",
      "priority": 2,
      "fetch_method": "direct",
      "method": "POST",
      "status": 1,
      "charset": "UTF-8",
      "charact_string_start": "",
      "charact_string_end": "",
      "pf_id": 1683,
      "data_out": "",
      "interval": "86400",
      "excluded_workers": "{excluded_workers}"
    },
    {
      "data_in": {
        "data_for_test": [
          {
            "link": "http://www.topfond.com/product/1.html",
            "drug_name": "硫酸阿米卡星注射液"
          }
        ]
      },
      "project_name": "{STU}.detail",
      "url": "{link}",
      "type": "one-off",
      "priority": 2,
      "fetch_method": "direct",
      "method": "GET",
      "status": 1,
      "charset": "UTF-8",
      "charact_string_start": "",
      "charact_string_end": "",
      "add_only": 1,
      "excluded_workers": "{excluded_workers}",
      "interval": 5184000,
      "data_out": {
        "jpath": "",
        "api": {
          "url": "http://api2.drugsea.cn/dp2/mongo/save",
          "table": "china_manufacture_products",
          "where": {
            "uniqueId": "{dp2_id}"
          },
          "data": {
            "dp2_id": "{dp2_id}",
            "drug_name": "{drug_name}",
            "manufacture": "{manufacture}",
            "attachments": "{attachments}",
            "content": "{content}"
          }
        }
      },
      "pf_id": 1684
    },
    {
      "data_in": {
        "jpath": "attachments",
        "data_for_test": {
          "attachments": [
            {
              "link": "http://www.topfond.com//repository/image/4e4f89b8-c6aa-4e74-a9d6-3535a649b752.jpg",
              "title": "阿米卡星注射液"
            }
          ]
        }
      },
      "project_name": "{STU}.attachments",
      "url": "{link}",
      "type": "one-off",
      "priority": 2,
      "fetch_method": "direct",
      "method": "GET",
      "status": 1,
      "charset": "UTF-8",
      "charact_string_start": "",
      "charact_string_end": "",
      "add_only": 1,
      "excluded_workers": "{excluded_workers}",
      "interval": 5184000,
      "pf_id": 1702,
      "data_out": {
        "jpath": "{key:key}",
        "api": {
          "url": "http://api2.drugsea.cn/dp2/mongo/save/v2",
          "table": "china_manufacture_products",
          "where": {
            "uniqueId": "{dp2_id}"
          },
          "data": {
            "data.attachments.{row_idx}.key": "{key}"
          }
        }
      }
    }
  ]
}
```



