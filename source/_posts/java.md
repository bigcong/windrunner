### 优雅读取文件

```
 List<String> lines = Files.readAllLines(Paths.get("/Users/cong/3.txt"), StandardCharsets
                .UTF_8);
```