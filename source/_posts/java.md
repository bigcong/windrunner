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

###  mybatis在xml文件中处理大于号小于号的方法

|       转义字符         |   字符          | 中文  |
| ------------- |:-------------:| -----:|
|    `&gt;`     |   >           |     大于号|
|    `&lt;`     |    <          |       小于号      |
|    `&apos;`   | ’             |     单引号 |
|    `&quot;`   |  "            |       双引号|

```
<![CDATA[ when min(starttime)<='12:00' and max(endtime)<='12:00' ]]>     
```


###  分组, 计数
```

    Map<string long> result =  
            items.stream().collect(  
                    Collectors.groupingBy(  
                            Function.identity(), Collectors.counting()  
                    )  
            ); 
```


### 排序

```

   int arr[] = {1, 4, 2, 8, 5};
        Arrays.parallelSort(arr);
        for(int i : arr){
            System.out.print(i + " ");
        }


```





