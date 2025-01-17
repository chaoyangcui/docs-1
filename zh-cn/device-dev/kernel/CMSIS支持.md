# CMSIS支持<a name="ZH-CN_TOPIC_0000001124074753"></a>

-   [基本概念](#section131091144111615)
-   [开发指导](#section57653573161)
    -   [接口说明](#section1795910417173)
    -   [开发流程](#section48301225131720)
    -   [编程实例](#section524434761713)


## 基本概念<a name="section131091144111615"></a>

[CMSIS](https://developer.arm.com/tools-and-software/embedded/cmsis)是Cortex Microcontroller Software Interface Standard（Cortex微控制器软件接口标准）的缩写，是对于那些基于ARM Cortex处理器的微控制器独立于供应商的硬件抽象层。它包含多个组件层，其中之一是RTOS层，该层定义了一套通用及标准化的RTOS API接口，减少了应用开发者对特定RTOS的依赖，方便用户软件的移植重用。该套API有2个版本，分别为版本1（CMSIS-RTOS v1）和版本2（CMSIS-RTOS v2），OpenHarmony LiteOS-M仅提供其版本2的实现。

## 开发指导<a name="section57653573161"></a>

### 接口说明<a name="section1795910417173"></a>

CMSIS-RTOS v2提供下面几种功能，接口详细信息可以查看API参考。

**表 1**  CMSIS-RTOS v2接口

<a name="table14277123518139"></a>
<table><thead align="left"><tr id="row152771935131315"><th class="cellrowborder" valign="top" width="17.77177717771777%" id="mcps1.2.4.1.1"><p id="p1127733591316"><a name="p1127733591316"></a><a name="p1127733591316"></a>功能分类</p>
</th>
<th class="cellrowborder" valign="top" width="23.782378237823785%" id="mcps1.2.4.1.2"><p id="p22771357138"><a name="p22771357138"></a><a name="p22771357138"></a>接口名</p>
</th>
<th class="cellrowborder" valign="top" width="58.44584458445845%" id="mcps1.2.4.1.3"><p id="p327714358130"><a name="p327714358130"></a><a name="p327714358130"></a>描述</p>
</th>
</tr>
</thead>
<tbody><tr id="row159539510586"><td class="cellrowborder" rowspan="13" valign="top" width="17.77177717771777%" headers="mcps1.2.4.1.1 "><p id="p1194410585810"><a name="p1194410585810"></a><a name="p1194410585810"></a>内核信息与控制</p>
</td>
<td class="cellrowborder" valign="top" width="23.782378237823785%" headers="mcps1.2.4.1.2 "><p id="p10944105115814"><a name="p10944105115814"></a><a name="p10944105115814"></a>osKernelGetInfo</p>
</td>
<td class="cellrowborder" valign="top" width="58.44584458445845%" headers="mcps1.2.4.1.3 "><p id="p9944105175818"><a name="p9944105175818"></a><a name="p9944105175818"></a>获取RTOS内核信息。</p>
</td>
</tr>
<tr id="row17953454580"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p2071181110424"><a name="p2071181110424"></a><a name="p2071181110424"></a>osKernelGetState</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p12388182124219"><a name="p12388182124219"></a><a name="p12388182124219"></a>获取当前的RTOS内核状态。</p>
</td>
</tr>
<tr id="row14587143217423"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p19587832194214"><a name="p19587832194214"></a><a name="p19587832194214"></a>osKernelGetSysTimerCount</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p17587193274218"><a name="p17587193274218"></a><a name="p17587193274218"></a>获取RTOS内核系统计时器计数。</p>
</td>
</tr>
<tr id="row6379429154617"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p63791299469"><a name="p63791299469"></a><a name="p63791299469"></a>osKernelGetSysTimerFreq</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p1037932924610"><a name="p1037932924610"></a><a name="p1037932924610"></a>获取RTOS内核系统计时器频率。</p>
</td>
</tr>
<tr id="row59815341465"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p898153494617"><a name="p898153494617"></a><a name="p898153494617"></a>osKernelInitialize</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p374817118497"><a name="p374817118497"></a><a name="p374817118497"></a>初始化RTOS内核。</p>
</td>
</tr>
<tr id="row11611104112469"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p861114144619"><a name="p861114144619"></a><a name="p861114144619"></a>osKernelLock</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p165481944917"><a name="p165481944917"></a><a name="p165481944917"></a>锁定RTOS内核调度程序。</p>
</td>
</tr>
<tr id="row36112411462"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p1461111416466"><a name="p1461111416466"></a><a name="p1461111416466"></a>osKernelUnlock</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p1767395194918"><a name="p1767395194918"></a><a name="p1767395194918"></a>解锁RTOS内核调度程序。</p>
</td>
</tr>
<tr id="row13482155394615"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p13483135312462"><a name="p13483135312462"></a><a name="p13483135312462"></a>osKernelRestoreLock</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p148385316469"><a name="p148385316469"></a><a name="p148385316469"></a>恢复RTOS内核调度程序锁定状态。</p>
</td>
</tr>
<tr id="row194831534464"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p11483115314615"><a name="p11483115314615"></a><a name="p11483115314615"></a>osKernelResume</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p1248319538464"><a name="p1248319538464"></a><a name="p1248319538464"></a>恢复RTOS内核调度程序。（暂未实现）</p>
</td>
</tr>
<tr id="row174831853134614"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p1483953184611"><a name="p1483953184611"></a><a name="p1483953184611"></a>osKernelStart</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p448312534464"><a name="p448312534464"></a><a name="p448312534464"></a>启动RTOS内核调度程序。</p>
</td>
</tr>
<tr id="row15483165384620"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p19483145320464"><a name="p19483145320464"></a><a name="p19483145320464"></a>osKernelSuspend</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p54831953194619"><a name="p54831953194619"></a><a name="p54831953194619"></a>挂起RTOS内核调度程序。（暂未实现）</p>
</td>
</tr>
<tr id="row13514125894616"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p0514175834615"><a name="p0514175834615"></a><a name="p0514175834615"></a>osKernelGetTickCount</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p4514258104611"><a name="p4514258104611"></a><a name="p4514258104611"></a>获取RTOS内核滴答计数。</p>
</td>
</tr>
<tr id="row951505817469"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p145151258124612"><a name="p145151258124612"></a><a name="p145151258124612"></a>osKernelGetTickFreq</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p1751545884611"><a name="p1751545884611"></a><a name="p1751545884611"></a>获取RTOS内核滴答频率。</p>
</td>
</tr>
<tr id="row79531357589"><td class="cellrowborder" rowspan="17" valign="top" width="17.77177717771777%" headers="mcps1.2.4.1.1 "><p id="p139443595820"><a name="p139443595820"></a><a name="p139443595820"></a>线程管理</p>
</td>
<td class="cellrowborder" valign="top" width="23.782378237823785%" headers="mcps1.2.4.1.2 "><p id="p1894435175815"><a name="p1894435175815"></a><a name="p1894435175815"></a>osThreadDetach</p>
</td>
<td class="cellrowborder" valign="top" width="58.44584458445845%" headers="mcps1.2.4.1.3 "><p id="p1194415518581"><a name="p1194415518581"></a><a name="p1194415518581"></a>分离线程（线程终止时可以回收线程存储）。（暂未实现）</p>
</td>
</tr>
<tr id="row1095320545814"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p20944355589"><a name="p20944355589"></a><a name="p20944355589"></a>osThreadEnumerate</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p169441515816"><a name="p169441515816"></a><a name="p169441515816"></a>枚举活动线程。（暂未实现）</p>
</td>
</tr>
<tr id="row44751341104510"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p1247514119454"><a name="p1247514119454"></a><a name="p1247514119454"></a>osThreadExit</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p368152110308"><a name="p368152110308"></a><a name="p368152110308"></a>终止当前正在运行的线程的执行。</p>
</td>
</tr>
<tr id="row13871526162611"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p88729267264"><a name="p88729267264"></a><a name="p88729267264"></a>osThreadGetCount</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p587222622618"><a name="p587222622618"></a><a name="p587222622618"></a>获取活动线程的数量。</p>
</td>
</tr>
<tr id="row343123212610"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p154313292610"><a name="p154313292610"></a><a name="p154313292610"></a>osThreadGetId</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p34317320269"><a name="p34317320269"></a><a name="p34317320269"></a>返回当前正在运行的线程的线程ID。</p>
</td>
</tr>
<tr id="row243133222613"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p16431132182613"><a name="p16431132182613"></a><a name="p16431132182613"></a>osThreadGetName</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p730821816303"><a name="p730821816303"></a><a name="p730821816303"></a>获取线程的名称。</p>
</td>
</tr>
<tr id="row962784718266"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p66271347192616"><a name="p66271347192616"></a><a name="p66271347192616"></a>osThreadGetPriority</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p1075615160301"><a name="p1075615160301"></a><a name="p1075615160301"></a>获取线程的当前优先级。</p>
</td>
</tr>
<tr id="row1627174752617"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p18627847122619"><a name="p18627847122619"></a><a name="p18627847122619"></a>osThreadGetStackSize</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p1162744718265"><a name="p1162744718265"></a><a name="p1162744718265"></a>获取线程的堆栈大小。</p>
</td>
</tr>
<tr id="row1862784732616"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p146271547162612"><a name="p146271547162612"></a><a name="p146271547162612"></a>osThreadGetStackSpace</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p16271047172619"><a name="p16271047172619"></a><a name="p16271047172619"></a>根据执行期间的堆栈水印记录获取线程的可用堆栈空间。</p>
</td>
</tr>
<tr id="row462774702618"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p26275475267"><a name="p26275475267"></a><a name="p26275475267"></a>osThreadGetState</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p25722137304"><a name="p25722137304"></a><a name="p25722137304"></a>获取线程的当前线程状态。</p>
</td>
</tr>
<tr id="row18515175322616"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p651565312611"><a name="p651565312611"></a><a name="p651565312611"></a>osThreadJoin</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p351555382611"><a name="p351555382611"></a><a name="p351555382611"></a>等待指定线程终止。（暂未实现）</p>
</td>
</tr>
<tr id="row4515115392620"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p85156534260"><a name="p85156534260"></a><a name="p85156534260"></a>osThreadNew</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p135151053142614"><a name="p135151053142614"></a><a name="p135151053142614"></a>创建一个线程并将其添加到活动线程中。</p>
</td>
</tr>
<tr id="row3515105319269"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p151514531263"><a name="p151514531263"></a><a name="p151514531263"></a>osThreadResume</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p423671023016"><a name="p423671023016"></a><a name="p423671023016"></a>恢复线程的执行。</p>
</td>
</tr>
<tr id="row14515115317264"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p12515185313263"><a name="p12515185313263"></a><a name="p12515185313263"></a>osThreadSetPriority</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p151515318261"><a name="p151515318261"></a><a name="p151515318261"></a>更改线程的优先级。</p>
</td>
</tr>
<tr id="row2516175314262"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p18516353122613"><a name="p18516353122613"></a><a name="p18516353122613"></a>osThreadSuspend</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p20829179301"><a name="p20829179301"></a><a name="p20829179301"></a>暂停执行线程。</p>
</td>
</tr>
<tr id="row0516165314267"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p6516125317262"><a name="p6516125317262"></a><a name="p6516125317262"></a>osThreadTerminate</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p95162537265"><a name="p95162537265"></a><a name="p95162537265"></a>终止线程的执行。</p>
</td>
</tr>
<tr id="row85168538268"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p5516653152615"><a name="p5516653152615"></a><a name="p5516653152615"></a>osThreadYield</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p65161534266"><a name="p65161534266"></a><a name="p65161534266"></a>将控制权传递给处于就绪状态的下一个线程。</p>
</td>
</tr>
<tr id="row119525513581"><td class="cellrowborder" rowspan="4" valign="top" width="17.77177717771777%" headers="mcps1.2.4.1.1 "><p id="p109442053586"><a name="p109442053586"></a><a name="p109442053586"></a>线程标志</p>
</td>
<td class="cellrowborder" valign="top" width="23.782378237823785%" headers="mcps1.2.4.1.2 "><p id="p9944354585"><a name="p9944354585"></a><a name="p9944354585"></a>osThreadFlagsSet</p>
</td>
<td class="cellrowborder" valign="top" width="58.44584458445845%" headers="mcps1.2.4.1.3 "><p id="p6407151912451"><a name="p6407151912451"></a><a name="p6407151912451"></a>设置线程的指定线程标志。（暂未实现）</p>
</td>
</tr>
<tr id="row55951654134512"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p12595125474520"><a name="p12595125474520"></a><a name="p12595125474520"></a>osThreadFlagsClear</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p195951854124518"><a name="p195951854124518"></a><a name="p195951854124518"></a>清除当前正在运行的线程的指定线程标志。（暂未实现）</p>
</td>
</tr>
<tr id="row1211243443217"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p1711210349323"><a name="p1711210349323"></a><a name="p1711210349323"></a>osThreadFlagsGet</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p161121934163213"><a name="p161121934163213"></a><a name="p161121934163213"></a>获取当前正在运行的线程的当前线程标志。（暂未实现）</p>
</td>
</tr>
<tr id="row1725104420324"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p62511944193212"><a name="p62511944193212"></a><a name="p62511944193212"></a>osThreadFlagsWait</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p3251134423219"><a name="p3251134423219"></a><a name="p3251134423219"></a>等待当前正在运行的线程的一个或多个线程标志发出信号。（暂未实现）</p>
</td>
</tr>
<tr id="row02511144123214"><td class="cellrowborder" rowspan="7" valign="top" width="17.77177717771777%" headers="mcps1.2.4.1.1 "><p id="p1525124443212"><a name="p1525124443212"></a><a name="p1525124443212"></a>事件标志</p>
</td>
<td class="cellrowborder" valign="top" width="23.782378237823785%" headers="mcps1.2.4.1.2 "><p id="p1251104415324"><a name="p1251104415324"></a><a name="p1251104415324"></a>osEventFlagsGetName</p>
</td>
<td class="cellrowborder" valign="top" width="58.44584458445845%" headers="mcps1.2.4.1.3 "><p id="p162511844123210"><a name="p162511844123210"></a><a name="p162511844123210"></a>获取事件标志对象的名称。（暂未实现）</p>
</td>
</tr>
<tr id="row135761548173211"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p145766484328"><a name="p145766484328"></a><a name="p145766484328"></a>osEventFlagsNew</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p19620209133718"><a name="p19620209133718"></a><a name="p19620209133718"></a>创建并初始化事件标志对象。</p>
</td>
</tr>
<tr id="row1257614803220"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p3576048193219"><a name="p3576048193219"></a><a name="p3576048193219"></a>osEventFlagsDelete</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p85761048153213"><a name="p85761048153213"></a><a name="p85761048153213"></a>删除事件标志对象。</p>
</td>
</tr>
<tr id="row35761248133212"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p1557744863216"><a name="p1557744863216"></a><a name="p1557744863216"></a>osEventFlagsSet</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p125772482328"><a name="p125772482328"></a><a name="p125772482328"></a>设置指定的事件标志。</p>
</td>
</tr>
<tr id="row5577174811327"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p25773487329"><a name="p25773487329"></a><a name="p25773487329"></a>osEventFlagsClear</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p1857704863218"><a name="p1857704863218"></a><a name="p1857704863218"></a>清除指定的事件标志。</p>
</td>
</tr>
<tr id="row4431856193218"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p344115673215"><a name="p344115673215"></a><a name="p344115673215"></a>osEventFlagsGet</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p1877255143717"><a name="p1877255143717"></a><a name="p1877255143717"></a>获取当前事件标志。</p>
</td>
</tr>
<tr id="row9441256183215"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p174485613213"><a name="p174485613213"></a><a name="p174485613213"></a>osEventFlagsWait</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p225211443712"><a name="p225211443712"></a><a name="p225211443712"></a>等待一个或多个事件标志被发出信号。</p>
</td>
</tr>
<tr id="row2441256113217"><td class="cellrowborder" rowspan="2" valign="top" width="17.77177717771777%" headers="mcps1.2.4.1.1 "><p id="p1644145614325"><a name="p1644145614325"></a><a name="p1644145614325"></a>通用等待函数</p>
</td>
<td class="cellrowborder" valign="top" width="23.782378237823785%" headers="mcps1.2.4.1.2 "><p id="p1844185619322"><a name="p1844185619322"></a><a name="p1844185619322"></a>osDelay</p>
</td>
<td class="cellrowborder" valign="top" width="58.44584458445845%" headers="mcps1.2.4.1.3 "><p id="p175964148382"><a name="p175964148382"></a><a name="p175964148382"></a>等待超时（时间延迟）。</p>
</td>
</tr>
<tr id="row1544185633211"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p944105617325"><a name="p944105617325"></a><a name="p944105617325"></a>osDelayUntil</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p944155663213"><a name="p944155663213"></a><a name="p944155663213"></a>等到指定时间。</p>
</td>
</tr>
<tr id="row1644185611327"><td class="cellrowborder" rowspan="6" valign="top" width="17.77177717771777%" headers="mcps1.2.4.1.1 "><p id="p154435610321"><a name="p154435610321"></a><a name="p154435610321"></a>计时器管理</p>
</td>
<td class="cellrowborder" valign="top" width="23.782378237823785%" headers="mcps1.2.4.1.2 "><p id="p1441956103217"><a name="p1441956103217"></a><a name="p1441956103217"></a>osTimerDelete</p>
</td>
<td class="cellrowborder" valign="top" width="58.44584458445845%" headers="mcps1.2.4.1.3 "><p id="p4460617134012"><a name="p4460617134012"></a><a name="p4460617134012"></a>删除计时器。</p>
</td>
</tr>
<tr id="row44418561329"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p244256133215"><a name="p244256133215"></a><a name="p244256133215"></a>osTimerGetName</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p111091116104011"><a name="p111091116104011"></a><a name="p111091116104011"></a>获取计时器的名称。（暂未实现）</p>
</td>
</tr>
<tr id="row14475617321"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p11449566322"><a name="p11449566322"></a><a name="p11449566322"></a>osTimerIsRunning</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p15171191510401"><a name="p15171191510401"></a><a name="p15171191510401"></a>检查计时器是否正在运行。</p>
</td>
</tr>
<tr id="row18451856123216"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p9452565322"><a name="p9452565322"></a><a name="p9452565322"></a>osTimerNew</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p7307131416401"><a name="p7307131416401"></a><a name="p7307131416401"></a>创建和初始化计时器。</p>
</td>
</tr>
<tr id="row77471003317"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p15747130123317"><a name="p15747130123317"></a><a name="p15747130123317"></a>osTimerStart</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p8300131334014"><a name="p8300131334014"></a><a name="p8300131334014"></a>启动或重新启动计时器。</p>
</td>
</tr>
<tr id="row1274720203310"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p207475018334"><a name="p207475018334"></a><a name="p207475018334"></a>osTimerStop</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p164211111114012"><a name="p164211111114012"></a><a name="p164211111114012"></a>停止计时器。</p>
</td>
</tr>
<tr id="row13747603334"><td class="cellrowborder" rowspan="6" valign="top" width="17.77177717771777%" headers="mcps1.2.4.1.1 "><p id="p135951430164112"><a name="p135951430164112"></a><a name="p135951430164112"></a>互斥管理</p>
</td>
<td class="cellrowborder" valign="top" width="23.782378237823785%" headers="mcps1.2.4.1.2 "><p id="p1774719019335"><a name="p1774719019335"></a><a name="p1774719019335"></a>osMutexAcquire</p>
</td>
<td class="cellrowborder" valign="top" width="58.44584458445845%" headers="mcps1.2.4.1.3 "><p id="p17748110103311"><a name="p17748110103311"></a><a name="p17748110103311"></a>获取互斥或超时（如果已锁定）。</p>
</td>
</tr>
<tr id="row57481033314"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p7748160133318"><a name="p7748160133318"></a><a name="p7748160133318"></a>osMutexDelete</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p1574811013313"><a name="p1574811013313"></a><a name="p1574811013313"></a>删除互斥对象。</p>
</td>
</tr>
<tr id="row1074810083314"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p37481018335"><a name="p37481018335"></a><a name="p37481018335"></a>osMutexGetName</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p1672310911423"><a name="p1672310911423"></a><a name="p1672310911423"></a>获取互斥对象的名称。（暂未实现）</p>
</td>
</tr>
<tr id="row774880143318"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p1774890163310"><a name="p1774890163310"></a><a name="p1774890163310"></a>osMutexGetOwner</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p1774880123313"><a name="p1774880123313"></a><a name="p1774880123313"></a>获取拥有互斥对象的线程。</p>
</td>
</tr>
<tr id="row474816043316"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p10748130133317"><a name="p10748130133317"></a><a name="p10748130133317"></a>osMutexNew</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p16203147194210"><a name="p16203147194210"></a><a name="p16203147194210"></a>创建并初始化Mutex对象。</p>
</td>
</tr>
<tr id="row1974830133315"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p1748405333"><a name="p1748405333"></a><a name="p1748405333"></a>osMutexRelease</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p138197519427"><a name="p138197519427"></a><a name="p138197519427"></a>释放由osMutexAcquire获取的Mutex。</p>
</td>
</tr>
<tr id="row16748605332"><td class="cellrowborder" rowspan="6" valign="top" width="17.77177717771777%" headers="mcps1.2.4.1.1 "><p id="p104749439424"><a name="p104749439424"></a><a name="p104749439424"></a>信号量</p>
</td>
<td class="cellrowborder" valign="top" width="23.782378237823785%" headers="mcps1.2.4.1.2 "><p id="p1374814018330"><a name="p1374814018330"></a><a name="p1374814018330"></a>osSemaphoreAcquire</p>
</td>
<td class="cellrowborder" valign="top" width="58.44584458445845%" headers="mcps1.2.4.1.3 "><p id="p15474643164212"><a name="p15474643164212"></a><a name="p15474643164212"></a>获取信号量令牌或超时（如果没有可用的令牌）。</p>
</td>
</tr>
<tr id="row157492013319"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p1874910023317"><a name="p1874910023317"></a><a name="p1874910023317"></a>osSemaphoreDelete</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p15749005333"><a name="p15749005333"></a><a name="p15749005333"></a>删除一个信号量对象。</p>
</td>
</tr>
<tr id="row1674919018338"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p3749140173315"><a name="p3749140173315"></a><a name="p3749140173315"></a>osSemaphoreGetCount</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p17836151144310"><a name="p17836151144310"></a><a name="p17836151144310"></a>获取当前信号量令牌计数。</p>
</td>
</tr>
<tr id="row67492012335"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p1474910043314"><a name="p1474910043314"></a><a name="p1474910043314"></a>osSemaphoreGetName</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p19131519124316"><a name="p19131519124316"></a><a name="p19131519124316"></a>获取信号量对象的名称。（暂未实现）</p>
</td>
</tr>
<tr id="row27499003313"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p19749110133315"><a name="p19749110133315"></a><a name="p19749110133315"></a>osSemaphoreNew</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p174920133315"><a name="p174920133315"></a><a name="p174920133315"></a>创建并初始化一个信号量对象。</p>
</td>
</tr>
<tr id="row16749150133310"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p1374970113311"><a name="p1374970113311"></a><a name="p1374970113311"></a>osSemaphoreRelease</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p1829193118439"><a name="p1829193118439"></a><a name="p1829193118439"></a>释放信号量令牌，直到初始最大计数。</p>
</td>
</tr>
<tr id="row1174915043319"><td class="cellrowborder" rowspan="9" valign="top" width="17.77177717771777%" headers="mcps1.2.4.1.1 "><p id="p169591053144317"><a name="p169591053144317"></a><a name="p169591053144317"></a>内存池</p>
</td>
<td class="cellrowborder" valign="top" width="23.782378237823785%" headers="mcps1.2.4.1.2 "><p id="p207492043320"><a name="p207492043320"></a><a name="p207492043320"></a>osMemoryPoolAlloc</p>
</td>
<td class="cellrowborder" valign="top" width="58.44584458445845%" headers="mcps1.2.4.1.3 "><p id="p17749808337"><a name="p17749808337"></a><a name="p17749808337"></a>从内存池分配一个内存块。</p>
</td>
</tr>
<tr id="row18749701334"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p1475018023312"><a name="p1475018023312"></a><a name="p1475018023312"></a>osMemoryPoolDelete</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p630111101441"><a name="p630111101441"></a><a name="p630111101441"></a>删除内存池对象。</p>
</td>
</tr>
<tr id="row14211207193314"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p3211071331"><a name="p3211071331"></a><a name="p3211071331"></a>osMemoryPoolFree</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p1362961674412"><a name="p1362961674412"></a><a name="p1362961674412"></a>将分配的内存块返回到内存池。</p>
</td>
</tr>
<tr id="row1421118783313"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p72111773318"><a name="p72111773318"></a><a name="p72111773318"></a>osMemoryPoolGetBlockSize</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p9868112814414"><a name="p9868112814414"></a><a name="p9868112814414"></a>获取内存池中的内存块大小。</p>
</td>
</tr>
<tr id="row6211674336"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p112121973338"><a name="p112121973338"></a><a name="p112121973338"></a>osMemoryPoolGetCapacity</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p19372103510449"><a name="p19372103510449"></a><a name="p19372103510449"></a>获取内存池中最大的内存块数。</p>
</td>
</tr>
<tr id="row321213733310"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p18212107203319"><a name="p18212107203319"></a><a name="p18212107203319"></a>osMemoryPoolGetCount</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p22125715338"><a name="p22125715338"></a><a name="p22125715338"></a>获取内存池中使用的内存块数。</p>
</td>
</tr>
<tr id="row421227113319"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p121212717338"><a name="p121212717338"></a><a name="p121212717338"></a>osMemoryPoolGetName</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p10212675330"><a name="p10212675330"></a><a name="p10212675330"></a>获取内存池对象的名称。</p>
</td>
</tr>
<tr id="row821219717330"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p182128733318"><a name="p182128733318"></a><a name="p182128733318"></a>osMemoryPoolGetSpace</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p1746455417441"><a name="p1746455417441"></a><a name="p1746455417441"></a>获取内存池中可用的内存块数。</p>
</td>
</tr>
<tr id="row1121218710331"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p021247123316"><a name="p021247123316"></a><a name="p021247123316"></a>osMemoryPoolNew</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p1750070144516"><a name="p1750070144516"></a><a name="p1750070144516"></a>创建并初始化一个内存池对象。</p>
</td>
</tr>
<tr id="row1121212743317"><td class="cellrowborder" rowspan="10" valign="top" width="17.77177717771777%" headers="mcps1.2.4.1.1 "><p id="p766918202458"><a name="p766918202458"></a><a name="p766918202458"></a>消息队列</p>
</td>
<td class="cellrowborder" valign="top" width="23.782378237823785%" headers="mcps1.2.4.1.2 "><p id="p142121175334"><a name="p142121175334"></a><a name="p142121175334"></a>osMessageQueueDelete</p>
</td>
<td class="cellrowborder" valign="top" width="58.44584458445845%" headers="mcps1.2.4.1.3 "><p id="p9155142917456"><a name="p9155142917456"></a><a name="p9155142917456"></a>删除消息队列对象。</p>
</td>
</tr>
<tr id="row1721217719337"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p13213271332"><a name="p13213271332"></a><a name="p13213271332"></a>osMessageQueueGet</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p17413163634510"><a name="p17413163634510"></a><a name="p17413163634510"></a>从队列获取消息，或者如果队列为空，则从超时获取消息。</p>
</td>
</tr>
<tr id="row62134710333"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p2021317743315"><a name="p2021317743315"></a><a name="p2021317743315"></a>osMessageQueueGetCapacity</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p162138719332"><a name="p162138719332"></a><a name="p162138719332"></a>获取消息队列中的最大消息数。</p>
</td>
</tr>
<tr id="row421315718337"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p92133723311"><a name="p92133723311"></a><a name="p92133723311"></a>osMessageQueueGetCount</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p174145104512"><a name="p174145104512"></a><a name="p174145104512"></a>获取消息队列中排队的消息数。</p>
</td>
</tr>
<tr id="row132133733314"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p192131274331"><a name="p192131274331"></a><a name="p192131274331"></a>osMessageQueueGetMsgSize</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p16243135844517"><a name="p16243135844517"></a><a name="p16243135844517"></a>获取内存池中的最大消息大小。</p>
</td>
</tr>
<tr id="row1921310713313"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p1421327153310"><a name="p1421327153310"></a><a name="p1421327153310"></a>osMessageQueueGetName</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p1590864164616"><a name="p1590864164616"></a><a name="p1590864164616"></a>获取消息队列对象的名称。（暂未实现）</p>
</td>
</tr>
<tr id="row121357193317"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p32135712333"><a name="p32135712333"></a><a name="p32135712333"></a>osMessageQueueGetSpace</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p165021611144610"><a name="p165021611144610"></a><a name="p165021611144610"></a>获取消息队列中消息的可用插槽数。</p>
</td>
</tr>
<tr id="row921377183320"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p10214972333"><a name="p10214972333"></a><a name="p10214972333"></a>osMessageQueueNew</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p9340131915465"><a name="p9340131915465"></a><a name="p9340131915465"></a>创建和初始化消息队列对象。</p>
</td>
</tr>
<tr id="row16214177103311"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p1214476332"><a name="p1214476332"></a><a name="p1214476332"></a>osMessageQueuePut</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p114312720466"><a name="p114312720466"></a><a name="p114312720466"></a>如果队列已满，则将消息放入队列或超时。</p>
</td>
</tr>
<tr id="row1621419719335"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p1821497183311"><a name="p1821497183311"></a><a name="p1821497183311"></a>osMessageQueueReset</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p12214276338"><a name="p12214276338"></a><a name="p12214276338"></a>将消息队列重置为初始空状态。（暂未实现）</p>
</td>
</tr>
</tbody>
</table>

### 开发流程<a name="section48301225131720"></a>

CMSIS-RTOS2组件可以作为库或源代码提供（下图显示了库）。通过添加CMSIS-RTOS2组件（通常是一些配置文件），可以将基于CMSIS的应用程序扩展为具有RTOS功能。只需包含cmsis\_os2.h头文件就可以访问RTOS API函数，这使用户应用程序能够处理RTOS内核相关事件，而在更换内核时无需重新编译源代码。

静态对象分配需要访问RTOS对象控制块定义。特定于实现的头文件（下图中的os\_xx .h）提供对此类控制块定义的访问。对于OpenHarmony LiteOS-M内核，由文件名以los\_开头的头文件提供，这些文件包含OpenHarmony LiteOS-M内核的这些定义。

![](figures/zh-cn_image_0000001121429646.png)

### 编程实例<a name="section524434761713"></a>

```
#include ...
#include "cmsis_os2.h"

/*----------------------------------------------------------------------------
 * 应用程序主线程
 *---------------------------------------------------------------------------*/
void app_main (void *argument) {
  // ...
  for (;;) {}
}

int main (void) {
  // 系统初始化
  MySystemInit();
  // ...

  osKernelInitialize();                 // 初始化CMSIS-RTOS
  osThreadNew(app_main, NULL, NULL);    // 创建应用程序主线程
  osKernelStart();                      // 开始执行线程
  for (;;) {}
}
```

