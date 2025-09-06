# 使用Node构建命令行工具

> 在用了Vue的脚手架工具以后，发现设计的非常好，简洁直观。因此，起念想要学习一下怎么使用Node来创建一个命令行工具

## Vue的脚手架工具

<p align = "center"><img width="400" height="500" alt="Image" src="https://github.com/user-attachments/assets/06cead0f-a8d2-425e-a6e4-052faf69e51b" /></p>

## 梳理

1. `package.json`：记录了Node项目的**基本信息**、**依赖**、**自定义脚本命令**

2. `CMD的命令查找`：先从**当前目录**中查找，（如果没有）再从系统的**环境变量PATH**中查找

## 逻辑

​	从Vue脚手架这个优秀的例子出发，在安装完Vue的脚手架工具以后，我们就可以在任何目录下，使用`npm create vue <project-name>`命令，就可以在当前目录下构建一个Vue项目。

​	首先，要实现这样的效果就要在`package.json`中添加`bin`配置项，添加后在使用`npm install -g <package-name>`安装后，npm会在系统环境变量**PATH中添加**我们在`bin`配置项中设置的**命令名称**，并且将这个**命令指向配置的js文件**，这样就可以在任意目录下面使用这个命令了

```json
{
    "bin":{
        "cli":'cli/index.js'
    }
}
```

​	其次，要实现**简洁直观的外观**，可以使用**第三方库**来方便的达到效果

​	最后，要注意**开发环境**和**生产环境**使用命令行工具的权限问题

​		**开发环境**：设置执行权限：`chmod +x bin/cli.js`

​		**生产环境**：npm会自行配置文件权限，确保可用

## 流程

1. 配置`package.json`

   ```json
   {
       "bin":{
           "cli":'cli/index.js'
       }
   }
   ```

2. 编写`index.js`文件

   ```js
   #! /usr/bin/env node
   
   //逻辑部分
   
   ```

3. 链接`npm link`，执行后就执行路径：`2 --- 3 --- PATH`

## 总结

### 使用场景

> 跨平台

1. 项目构建工具
2. 自动化
3. 数据处理

### 三方库（美化）


<table align = "center">
    <tr>
    	<th colspan="2" align = "center">字体样式</th>
    </tr>
    <tr>
        <td align = "center">chalk</td>
        <td align = "center">colorette(小体积)</td>
    </tr>
	<tr>
        <td align = "center">
            <table>
            	<tr>
                	<td align = "center">简介</td>
                    <td align = "center">粗体、下划线、背景色</td>
                </tr>
				<tr>
                	<td align = "center">导入</td>
                    <td align = "center">
                    	import chalk from "chalk"
                    </td>
                </tr>
                <tr>
                	<td align = "center">地址</td>
                    <td align = "center"><a>https://www.npmjs.com/package/chalk</a></td>
                </tr>
            </table>
        </td>
        <td align = "center">
            <table>
            	<tr>
                	<td align = "center">简介</td>
                    <td align = "center">chalk的简化版本，粗体、下划线、背景色</td>
                </tr>
				<tr>
                	<td align = "center">最小构建</td>
                    <td align = "center">
                    	import { blue, bold, underline } from "colorette"
                    </td>
                </tr>
                <tr>
                	<td align = "center">地址</td>
                    <td align = "center"><a>https://www.npmjs.com/package/colorette</a></td>
                </tr>
            </table>
        </td>
    </tr>
</table>
<table align = "center">
    <tr>
    	<th align = "center">参数解析</th>
    </tr>
    <tr>
        <td align = "center">commander</td>
    </tr>
	<tr>
        <td align = "center">
            <table>
            	<tr>
                	<td align = "center">简介</td>
                    <td align = "center">用来处理命令、参数、选项，自动生成帮助信息</td>
                </tr>
				<tr>
                	<td align = "center">导入</td>
                    <td align = "center">
                    	import { Command } from "commander"
						const program = new Command()
                    </td>
                </tr>
                <tr>
                	<td align = "center">地址</td>
                    <td align = "center"><a>https://www.npmjs.com/package/commander</a></td>
                </tr>
            </table>
        </td>
    </tr>
</table>

<table align = "center">
    <tr>
    	<th colspan="2" align = "center">动态效果</th>
    </tr>
    <tr>
        <td align = "center">cli-progress</td>
        <td align = "center">ora</td>
    </tr>
	<tr>
        <td align = "center">
            <table>
            	<tr>
                	<td align = "center">简介</td>
                    <td align = "center">进度条</td>
                </tr>
				<tr>
                	<td align = "center">使用</td>
                    <td align = "center">
                    	import { SingleBar, Presets } from "cli-progress"
                    </td>
                </tr>
                <tr>
                	<td align = "center">地址</td>
                    <td align = "center"><a>https://www.npmjs.com/package/cli-progress</a></td>
                </tr>
            </table>
        </td>
        <td align = "center">
            <table>
            	<tr>
                	<td align = "center">简介</td>
                    <td align = "center">加载动画</td>
                </tr>
				<tr>
                	<td align = "center">使用</td>
                    <td align = "center">
                        import ora from 'ora'
                    </td>
                </tr>
                <tr>
                	<td align = "center">地址</td>
                    <td align = "center"><a>https://www.npmjs.com/package/ora</a></td>
                </tr>
            </table>
        </td>
    </tr>
</table>

<table align = "center">
    <tr>
    	<th align = "center">表格</th>
    </tr>
    <tr>
        <td align = "center">cli-table3</td>
    </tr>
	<tr>
        <td align = "center">
            <table>
            	<tr>
                	<td align = "center">简介</td>
                    <td align = "center">表格显示数据，让结构更清晰</td>
                </tr>
				<tr>
                	<td align = "center">导入</td>
                    <td align = "center">
                    	import Table from "cli-table3"
                    </td>
                </tr>
                <tr>
                	<td align = "center">地址</td>
                    <td align = "center"><a>https://www.npmjs.com/package/cli-table3</a></td>
                </tr>
            </table>
        </td>
    </tr>
</table>

<table align = "center">
    <tr>
    	<th align = "center">艺术字</th>
    </tr>
    <tr>
        <td align = "center">figlet</td>
    </tr>
	<tr>
        <td align = "center">
            <table>
            	<tr>
                	<td align = "center">简介</td>
                    <td align = "center">打印醒目的标题</td>
                </tr>
				<tr>
                	<td align = "center">导入</td>
                    <td align = "center">
                    	import figlet from "figlet"
                    </td>
                </tr>
                <tr>
                	<td align = "center">地址</td>
                    <td align = "center"><a>https://www.npmjs.com/package/figlet</a></td>
                </tr>
            </table>
        </td>
    </tr>
</table>

<table align = "center">
    <tr>
    	<th align = "center">交互式输入</th>
    </tr>
    <tr>
        <td align = "center">figlet</td>
    </tr>
	<tr>
        <td align = "center">
            <table>
            	<tr>
                	<td align = "center">简介</td>
                    <td align = "center">选择菜单、确认、输入框</td>
                </tr>
				<tr>
                	<td align = "center">导入</td>
                    <td align = "center">
                    	import inquirer from "inquirer"
                    </td>
                </tr>
                <tr>
                	<td align = "center">地址</td>
                    <td align = "center"><a>https://www.npmjs.com/package/inquirer</a></td>
                </tr>
            </table>
        </td>
    </tr>
</table>