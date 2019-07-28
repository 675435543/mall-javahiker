mall04-jwt 工程完全参考作者下面的教程搭建
- [mall整合SpringSecurity和JWT实现认证和授权（一）](https://juejin.im/post/5cf90fa5e51d455d6d5357d3)
- [mall整合SpringSecurity和JWT实现认证和授权（二）](https://juejin.im/post/5cfa0933f265da1b8f1ab2da)

介绍jwt的一篇博文
- [认识JWT](https://www.cnblogs.com/cjsblog/p/9277677.html)

给PmsBrandController接口中的方法添加访问权限
- 给查询接口添加pms:brand:read权限
- 给修改接口添加pms:brand:update权限
- 给删除接口添加pms:brand:delete权限
- 给添加接口添加pms:brand:create权限


    @PreAuthorize("hasAuthority('pms:brand:read')")
    public CommonResult<List<PmsBrand>> getBrandList() {
        return CommonResult.success(brandService.listAllBrand());
    }
