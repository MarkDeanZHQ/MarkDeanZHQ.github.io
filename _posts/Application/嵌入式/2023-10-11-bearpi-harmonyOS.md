---
categories: [Application, Embedded]
tag: [embedded_dev, C, bearpi_harmonyOS]
---
# 2023-10-11-bearpi-harmonyOS

office_link:[bearpi-hm_nano](https://gitee.com/bearpi/bearpi-hm_nano)

## Preparation
1. image：下载地址（百度云）：https://pan.baidu.com/s/1T0Tcl3y48C1p5L6y-6HJNg 提取码：eusr
2. HiBurn：下载地址（百度云）：https://pan.baidu.com/s/1bp2ypAfH2HaNPTY2KwEhEA 提取码：1234
3. VMware Workstation
4. MobaXterm
5. RaiDrive
6. USB drive：http://www.wch.cn/search?q=ch340g&t=downloads
7. VS Code


### get and compile the source code
on project root directory

Method one (from gitee)
```bash
git clone https://gitee.com/bearpi/bearpi-hm_nano.git -b master   // get
python build.py BearPi-HM_Nano  // compile
```  
  
Method two (by hpm)
```bash
hpm init -t default
hpm i @bearpi/bearpi_hm_nano  //get source code

hpm dist // compile code 
```


And `projeck/out/BearPi-HM_Nano`{: .filepath} is the path of bin file.

### Burn
![HiBurn%E4%B8%BB%E7%95%8C%E9%9D%A2](https://raw.githubusercontent.com/MarkDeanZHQ/ImageHost/main/zhq_shack/_posts/2023-10-11-bearpi-harmonyos.md/291831518254292.png)
![HiBurn_Comsettings](https://raw.githubusercontent.com/MarkDeanZHQ/ImageHost/main/zhq_shack/_posts/2023-10-11-bearpi-harmonyos.md/167661718247838.png)
![HiBurn_%E6%89%93%E5%BC%80%E6%96%87%E4%BB%B6](https://raw.githubusercontent.com/MarkDeanZHQ/ImageHost/main/zhq_shack/_posts/2023-10-11-bearpi-harmonyos.md/390651718240972.png)

At this time press the reset button
![%E5%A4%8D%E4%BD%8D%E5%BC%80%E5%8F%91%E6%9D%BF](https://raw.githubusercontent.com/MarkDeanZHQ/ImageHost/main/zhq_shack/_posts/2023-10-11-bearpi-harmonyos.md/365161818234006.png)![HiBurn%E5%87%86%E5%A4%87%E4%B8%8B%E8%BD%BD](https://raw.githubusercontent.com/MarkDeanZHQ/ImageHost/main/zhq_shack/_posts/2023-10-11-bearpi-harmonyos.md/599641718231502.png)

![Hiburn_%E4%B8%8B%E8%BD%BD%E7%A8%8B%E5%BA%8F%E4%B8%AD](https://raw.githubusercontent.com/MarkDeanZHQ/ImageHost/main/zhq_shack/_posts/2023-10-11-bearpi-harmonyos.md/247241918242953.png)

### View the serial port and print log 
![Mobax_Serial_%E9%80%89%E6%8B%A9](https://raw.githubusercontent.com/MarkDeanZHQ/ImageHost/main/zhq_shack/_posts/2023-10-11-bearpi-harmonyos.md/575961918235838.png)

![COM%E5%90%AF%E5%8A%A8%E6%97%A5%E5%BF%97](https://raw.githubusercontent.com/MarkDeanZHQ/ImageHost/main/zhq_shack/_posts/2023-10-11-bearpi-harmonyos.md/111232018236447.png)


## Compilation Instructions

### directory structure
work directory: ./applications/BearPi/BearPi-HM_Nano/sample/{my_app}  
required file: file.c, BUILD.gn

#### example - hello_world  follows:

- my_app
    - file.c
    - BUILD.gn
    
```c
#include <stio.h>
#include "ohos_init.h" // APP_define head_file

void Hello_Wolrd(void)
{
    printf("Hello World! \r\n");
}
APP_FEATURE_INIT(Hello_World); // call the function when init

```
{: file='my_app/file.c'}
  



```java
static_library("myapp") {
    sources = [
        "hello_world.c"      
    ]
    include_dirs = [
        "//utils/native/lite/include"
    ]
}
```
{: file='my_app/BUILD.gn'}

* **static_library** specify the result of compilation and that is libmyapp.a
* **sources** specify  .c file depent by static_library .a. And "//" means absolute path otherwise relative path.
* **include_dirs** specify the path of .h file


- edit the module file BUILD.gn   
add the following code

```java
import("//build/lite/config/component/lite_component.gni")

lite_component("app") {
    features = [
        "my_app:myapp"
        ]
}
```
{: file='./applications/BearPi/BearPi-HM/sample/.BUILD.gn}

* **my_app** is relative path. 
* **myapp** is target wich refer to static_library{"myapp"} in my_app/BUILD.gn



## Ninja introduction
file convert & link : .c -> .a -> .bin




## task related conception
![task related](https://raw.githubusercontent.com/MarkDeanZHQ/ImageHost/main/zhq_shack/_posts/2023-10-11-bearpi-harmonyos.md/585790316231059.png)

### manage thread
![manage thread](https://raw.githubusercontent.com/MarkDeanZHQ/ImageHost/main/zhq_shack/_posts/2023-10-11-bearpi-harmonyos.md/404200516249485.png)

### mechanism of thread
![mechanism](https://raw.githubusercontent.com/MarkDeanZHQ/ImageHost/main/zhq_shack/_posts/2023-10-11-bearpi-harmonyos.md/387230616237352.png)


### create thread interface
![create thread](https://raw.githubusercontent.com/MarkDeanZHQ/ImageHost/main/zhq_shack/_posts/2023-10-11-bearpi-harmonyos.md/268540816257518.png)


### example
```c
#include <stdio.h>
#include <string.h>
#include <unistd.h>

#include "ohos_init.h"
#include "cmsis_os2.h"
#include "wifiiot_gpio.h"
#include "wifiiot_gpio_ex.h"

void thread1(void)
{
    int sum = 0;
    while (1)
    {
        printf("This is Led Thread1----%d\r\n", sum++);
        GpioSetOutputVal(WIFI_IOT_IO_NAME_GPIO_2, 1);
        usleep(1000000);
        GpioSetOutputVal(WIFI_IOT_IO_NAME_GPIO_2,0);
        usleep(1000000);
    }
}

void thread2(void)
{
    int sum = 0;
    while (1)
    {
        printf("This is BearPi Harmony Thread2----%d\r\n", sum++);
        usleep(500000); //延时0.5s
    }
}

static void Thread_example(void)
{
    GpioInit();
    IoSetFunc(WIFI_IOT_IO_NAME_GPIO_2,WIFI_IOT_IO_FUNC_GPIO_2_GPIO);
    GpioSetDir(WIFI_IOT_IO_NAME_GPIO_2,WIFI_IOT_GPIO_DIR_OUT);
    osThreadAttr_t attr;

    attr.name = "thread1";
    attr.attr_bits = 0U; // decide if osThreadJoin can be used: 0U means off & 1U means on
    attr.cb_mem = NULL; // set the pointer to control block
    attr.cb_size = 0U;
    attr.stack_mem = NULL;// set the pointer to control stack
    attr.stack_size = 1024 * 4;
    attr.priority = 25; 

    if (osThreadNew((osThreadFunc_t)thread1, NULL, &attr) == NULL)
    {
        printf("Falied to create thread1!\n");
    }

    attr.name = "thread2";

    if (osThreadNew((osThreadFunc_t)thread2, NULL, &attr) == NULL)
    {
        printf("Falied to create thread2!\n");
    }
}
APP_FEATURE_INIT(Thread_example);
```
{: .file='my_thread/thread.c'}

```java
static_library("mythread") {
    sources = [
        "thread.c"     
    ]

    include_dirs = [
        "//utils/native/lite/include",   // printf
        "//kernel/liteos_m/components/cmsis/2.0",  // thread
        "//base/iot_hardware/interfaces/kits/wifiiot_lite" // led light
    ]
}

```
{: file='my_thread/BUILD.gn' }

