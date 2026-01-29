# ESP32-study

## 简介
记录ESP32学习过程 | 包括环境搭建、基础外设、网络、蓝牙等案例

## 学习路径 
- ESP32快速入门开发秘籍（IDF版)：  
  https://www.bilibili.com/video/BV1EPisBWEUX/

## 环境搭建

### IDF

下载路径：https://dl.espressif.cn/dl/esp-idf/

使用版本：ESP-IDF v5.5.2  

1. 安装完成后打开ESP-IDF 5.5 PowerShell或CMD  
   显示如图则代表安装成功
   ![PowerShell运行结果](assets/屏幕截图%202026-01-28%20155036.png)

2. 设置环境变量
   右键 ` 此电脑 `, 点击 ` 属性 `, 选择 ` 高级系统设置` 中的 ` 环境变量 `

   ![设置变量操作1](assets/屏幕截图%202026-01-28%20162619.png)

   点击 ` 用户变量 ` 的 ` 新建 `, 变量名设置为 ` IDF_PAHTH `, 变量值可点击 ` 浏览目录 `找到IDF安装路径里的 ` frameworks/esp-idf-v5.5.2 `

   ![设置变量操作2](assets/0073055e-9a84-4826-adc3-a73ea625e5d9.png)

   确定

常用ESP-IDF命令
|功能|命令|说明|
|:---:|:---|:---|
|创建新工程|idf.py create-project --path &lt;project name&gt;|默认工程为esp32|
|设置目标芯片|idf.py set-target &lt;target&gt;|esp32s3、esp32p4|
|创建新的组件|idf.py create-component &lt;component name&gt;|创建外设驱动|
|编译工程|idf.py build|
|监控项目工程|idf.py monitor|退出监控 ` Ctrl + ] `|
|配置项目|idf.py menuconfig|项目配置|
|下载程序|idf.py -p COMx flash|x为端口号|
|清除编译文件|idf.py fullclean; idf.py clean|全部清除; 部分清除|

### VSCode环境搭建
1. 打开 ` VSCode `, 搜索插件 ` ESP-IDF `并安装
   ![ESP-IDF插件](assets/image.png)

2. 进入到 ` ESP-IDE Welcome `， 点击 ` Configure extention `
   ![VSCode环境搭建操作1](assets/image-1.png)

3. 进入到 ` ESP-IDF 设置 `, 点击 ` USE EXISTING SETUP `后选择 ` 版本 `
   ![VSCode环境搭建操作2](assets/8460812768172bfcd441c3fcfc59778b.png)
   ![VSCode环境搭建操作3](assets/7d6d53fc5ddd7251fe71c5cee3f82ae5.png)

## 新建工程
1. 在IDF安装目录下找到 ` sample_project `, 路径为 ` Espressif\frameworks\esp-idf-v5.5.2\tools\templates `, 复制到 ` Espressif\frameworks\esp-idf-v5.5.2\examples\get-started\ `目录下, 为后续工程提供模板
   ![新建工程操作1](assets/新建工程1.png)
   ![新建工程操作2](assets/新建工程2.png)

2. 打开VSCode, 按 ` Ctrl ` + ` Shift ` + ` P `, 搜索 ` 新建项目 `, 选择 ` ESP-IDF: 新建项目 `, 等待加载完成后选择 ` 框架 `
   ![新建工程操作3](assets/新建工程3.png)

3. 设置工程文件信息
   ![新建工程操作4](assets/新建工程4.png)
   ①项目名称
   ②存储路径
   ③选择芯片型号
   ④下载方式
   ⑤串口号
   设置完成后点击 ` Choose Template ` 选择模板

4. 在 ` get-started ` 中选择 ` sample_project `, 点击 ` Create `
   ![新建工程操作5](assets/新建工程5.png)
   右下角选择 `YES`, 在新窗口打开, 其他忽略

5. 初始化配置
- 在下边栏中点击 ` menuconfig `
   加载完成后, 在 ` 搜索框 `搜索 ` cpu `, 配置CPU主频率
   ![新建工程操作6](assets/新建工程6.png)

- 配置 ` flash `
   ![新建工程操作7](assets/新建工程7.png)
   ①搜索 ` flash `
   ②选择 ` QIO `模式, 要比 `DIO`快
   ③选择 ` flash ` 的 ` SPI频率 `
   ④选择 ` 容量 `

- 配置 ` psram `
   ![新建工程操作8](assets/新建工程8.png)

- 设置 `tick clock 频率 `为1000Hz, 方便后续使用 `延时函数` `(vTaskDelay)`
   ![新建工程操作9](assets/新建工程9.png)

- 配置分区表
  ![新建工程操作10](assets/新建工程10.png)
  ①搜索 `partition table`
  ②Custom partition table CSV 自定义分区表
  ③命名
  ④保存
  ⑤删掉旧的分区表

  ` Ctrl ` + ` Shift ` + ` P ` 搜索 ` 分区 `, 选择 `打开分区表编辑器UI`
  ![新建工程操作11](assets/新建工程11.png)

  ![新建工程操作12](assets/新建工程12.png)
  ①添加新的分区
  ②配置如图
  ③保存
- 工程新建完毕，点击 `编译`, no problem
  ![新建工程操作13](assets/新建工程13.png)
