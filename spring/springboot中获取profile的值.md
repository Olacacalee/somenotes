### spring boot中获取profile

```
@Autowired
private ApplicationContext context;

String profile = context.getEnvironment().getActiveProfiles()[0]
```