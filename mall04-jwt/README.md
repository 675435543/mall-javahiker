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

客户端和服务器之间的交互
- 客户端根据用户名和密码访问服务器
- 服务器验证通过后返回一个token给客户端
- 客户端以后每次都带着这个token去访问服务器
- 服务器根据token确定用户是否登录过期，以及是否具有访问权限

对于登录授权过滤器
首先所有的请求，包括"/admin/register"和"/admin/login",都会走到JwtAuthenticationTokenFilter的方法doFilterInternal()里面来
- 在SecurityConfig 里面配置的允许访问的请求.antMatchers("/admin/login", "/admin/register").permitAll()，会直接放过
- 其余请求都会被拦截下来，根据token去验证用户登录是否过期
- 如果有权限验证的还需要验证用户是否具有访问权限

这里请求被分成了三种
- 允许访问的请求，/admin/login，/admin/register
- 需要有token并且token未过期，不需要权限的
- 需要有token并且token未过期，需要有访问权限的，如读权限 @PreAuthorize("hasAuthority('pms:brand:read')")

