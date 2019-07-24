## mall-swagger-ui 工程完全参考作者下面的教程搭建
+ [mall整合Swagger-UI实现在线API文档](https://juejin.im/post/5cf9035cf265da1bb47d54f8)


    注意点
    为当前包下controller生成API文档
    .apis(RequestHandlerSelectors.basePackage("com.macro.mall.tiny.controller"))
    为有@Api注解的Controller生成API文档
    .apis(RequestHandlerSelectors.withClassAnnotation(Api.class))
    为有@ApiOperation注解的方法生成API文档
    .apis(RequestHandlerSelectors.withMethodAnnotation(ApiOperation.class))
    一种链式写法，如果同时打开的话就是取交集，3个条件同时满足时才会有对应方法的在线API文档
    它们从controller层，类，方法三个不同层面对在线API文档的生成做了控制



