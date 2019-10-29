使用Junit测试Controller类时出现了service无法自动注入，空指针异常问题，但是运行主函数可正常注入。于是判断问题应该出在测试类里。走了很多弯路后发现测试类中也要自动装配Controller类，解决方法如下：

> 源代码
```
@Before
public void setUp() throws Exception {
    mvc = MockMvcBuilders.standaloneSetup(new UserController()).build();
}
```
> 改动后
```
@Autowired
private UserController usercontroller;

@Before
public void setUp() throws Exception {
    mvc = MockMvcBuilders.standaloneSetup(usercontroller).build();
}
```
