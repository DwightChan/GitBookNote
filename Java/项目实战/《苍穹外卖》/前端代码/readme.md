<!--
 * @Author: Dwight Dwight@gmail.com
 * @Date: 2024-11-03 17:39:39
 * @LastEditors: Dwight Dwight@gmail.com
 * @LastEditTime: 2024-11-03 17:40:08
 * @FilePath: /GitBookNote/Java/项目实战/《苍穹外卖》/前端代码/readme.md
 * @Description: 这是默认设置,请设置`customMade`, 打开koroFileHeader查看配置 进行设置: https://github.com/OBKoro1/koro1FileHeader/wiki/%E9%85%8D%E7%BD%AE
-->


Sky 文件夹是 前端 编译后的代码
通过 nginx 配置服务 既可以直接运行
本电脑 配置了 端口地址 8999

localhost:8999

nginx -t   # 测试配置文件语法
brew services restart nginx   # 重启 Nginx 服务

**注意：前端代码不要配置在中文目录下**