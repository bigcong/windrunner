title: java代码
date: 2017-08-24 16:48:37
---

---
### 优雅读取文件

```
 List<String> lines = Files.readAllLines(Paths.get("/Users/cong/3.txt"), StandardCharsets
                .UTF_8);
```


### list to Map (java 8)
```
        Map<String, String> collect = caBankTypeService.listCaBankType(new CaBankType()).stream().collect(Collectors.toMap(CaBankType::getBankUuid, CaBankType::getBankCenterName));


```