# Shiro + JWT + SpringBoot + MySQL + Redis(Jedis)实现无状态鉴权机制(Restful风格API)

## 序言

首先感谢SmithCruise提供的思路，文章地址：[https://www.jianshu.com/p/f37f8c295057](https://www.jianshu.com/p/f37f8c295057)<br/>

根据SmithCruise的项目进行后续更新<br/>
* 将其改为数据库形式(MySQL)
* 实现Shiro的Cache(Redis)功能
* 解决无法直接返回401错误
* Token刷新(RefreshToken)

我的项目地址
* Github：[https://github.com/wang926454/ShiroJwt](https://github.com/wang926454/ShiroJwt)
* Gitee(码云)：[https://gitee.com/wang926454/ShiroJwt](https://gitee.com/wang926454/ShiroJwt)

## 目录

* 将其改为数据库形式(MySQL)：[https://blog.csdn.net/wang926454/article/details/82971442](https://blog.csdn.net/wang926454/article/details/82971442)
* 解决无法直接返回401错误：[https://blog.csdn.net/wang926454/article/details/82971846](https://blog.csdn.net/wang926454/article/details/82971846)
* 实现Shiro的Cache(Redis)功能：[https://blog.csdn.net/wang926454/article/details/82978632](https://blog.csdn.net/wang926454/article/details/82978632)