# Java 操作yaml和json之间的互相转换

> 1. json转yaml
```
 /**
     * 將json轉化為yaml格式并生成yaml文件
     * @param jsonString
     * @return
     * @throws JsonProcessingException
     * @throws IOException
     */
    @SuppressWarnings("unchecked")
    public static void createYaml(String yaml_url,String jsonString) throws JsonProcessingException, IOException {
        // parse JSON
        JsonNode jsonNodeTree = new ObjectMapper().readTree(jsonString);
        // save it as YAML
        String jsonAsYaml = new YAMLMapper().writeValueAsString(jsonNodeTree);

        Yaml yaml = new Yaml();
        Map<String,Object> map = (Map<String, Object>) yaml.load(jsonAsYaml);

        createYamlFile(yaml_url, map);
    }
```
> 2. yaml转map
```
 /**
      * 将yaml文件内容转为Map
      * @param filePath
      * @return: java.util.Map<java.lang.String,java.lang.Object>
      * @author tianyamoke
      * @date 2019/10/25 下午5:35
      */
     private static Map<String,Object> yamlToMap(String filePath){
         try {
             Yaml yaml = new Yaml();
             File dumpFile = new File(filePath);
             Map<String, Object> map =(Map<String, Object>)yaml.load(new FileInputStream(dumpFile));
             return map;
         }catch (Exception e){
             e.printStackTrace();
         }
         return null;
     }

```
> map转yaml
```
/**
     * 创建yaml文件
     * @param filePath
     * @param map
     * @return: void
     * @author tianyamoke
     * @date 2019/10/23 下午6:42
     */
    private static void writeToYaml(String filePath,Map<String,Object> map){
        try{
            DumperOptions dumperOptions = new DumperOptions();
            dumperOptions.setDefaultFlowStyle(DumperOptions.FlowStyle.BLOCK);
            Yaml yaml1 = new Yaml(dumperOptions);
            File df = new File(filePath);
            FileWriter fileWriter = new FileWriter(df);
            yaml1.dump(map, fileWriter);
            fileWriter.close();
        }catch (IOException e){
            e.printStackTrace();
        }
    }
```

