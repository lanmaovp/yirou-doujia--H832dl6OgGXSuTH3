
## 获取应用文件路径


基类Context提供了获取应用文件路径的能力，ApplicationContext、AbilityStageContext、UIAbilityContext和ExtensionContext均继承该能力。应用文件路径属于应用沙箱路径，上述各类Context获取的应用文件路径有所不同。


通过ApplicationContext获取应用级别的应用文件路径，此路径是应用全局信息推荐的存放路径，这些文件会跟随应用的卸载而删除




| 属性 | 路径 |
| --- | --- |
| bundleCodeDir | \<路径前缀\>/el1/bundle |
| cacheDir | \<路径前缀\>/\<加密等级\>/base/cache |
| filesDir | \<路径前缀\>/\<加密等级\>/base/files |
| preferencesDir | \<路径前缀\>/\<加密等级\>/base/preferences |
| tempDir | \<路径前缀\>/\<加密等级\>/base/temp |
| databaseDir | \<路径前缀\>/\<加密等级\>/database |
| distributedFilesDir | \<路径前缀\>/el2/distributedFiles |
| cloudFileDir | \<路径前缀\>/el2/cloud |


通过AbilityStageContext、UIAbilityContext、ExtensionContext获取HAP级别的应用文件路径。此路径是HAP相关信息推荐的存放路径，这些文件会跟随HAP的卸载而删除，但不会影响应用级别路径的文件，除非该应用的HAP已全部卸载




| 属性 | 路径 |
| --- | --- |
| bundleCodeDir | \<路径前缀\>/el1/bundle |
| cacheDir | \<路径前缀\>/\<加密等级\>/base/haps//cache |
| filesDir | \<路径前缀\>/\<加密等级\>/base/haps//files |
| preferencesDir | \<路径前缀\>/\<加密等级\>/base/haps//preferences |
| tempDir | \<路径前缀\>/\<加密等级\>/base/haps//temp |
| databaseDir | \<路径前缀\>/\<加密等级\>/database/ |
| distributedFilesDir | \<路径前缀\>/el2/distributedFiles/ |
| cloudFileDir | \<路径前缀\>/el2/cloud/ |


## 获取和修改加密分区


应用文件加密是一种保护数据安全的方法，可以使得文件在未经授权访问的情况下得到保护。在不同的场景下，应用需要不同程度的文件保护。在实际应用中，开发者需要根据不同场景的需求选择合适的加密分区，从而保护应用数据的安全。通过合理使用不同级别的加密分区，可以有效提高应用数据的安全性。


* EL1：对于私有文件，如闹铃、壁纸等，应用可以将这些文件放到设备级加密分区（EL1）中，以保证在用户输入密码前就可以被访问。
* EL2：对于更敏感的文件，如个人隐私信息等，应用可以将这些文件放到更高级别的加密分区（EL2）中，以保证更高的安全性。
* EL3：对于应用中的记录步数、文件下载、音乐播放，需要在锁屏时读写和创建新文件，放在（EL3）的加密分区比较合适。
* EL4：对于用户安全信息相关的文件，锁屏时不需要读写文件、也不能创建文件，放在（EL4）的加密分区更合适。
* EL5：对于用户隐私敏感数据文件，锁屏后默认不可读写，如果锁屏后需要读写文件，则锁屏前可以调用Access接口申请继续读写文件，或者锁屏后也需要创建新文件且可读写，放在（EL5）的应用级加密分区更合适


## 获取本应用中其他module的context


调用createModuleContext(moduleName:string)方法，获取本应用中其他Module的Context。获取到其他Module的Context之后，即可获取到相应Module的资源信息。


## 订阅进程内UIAbility生命周期变化


在应用内的DFX统计场景中，如需要统计对应页面停留时间和访问频率等信息，可以使用订阅进程内UIAbility生命周期变化功能。


通过ApplicationContext提供的能力，可以订阅进程内UIAbility生命周期变化。当进程内的UIAbility生命周期变化时，如创建、可见/不可见、获焦/失焦、销毁等，会触发相应的回调函数。每次注册回调函数时，都会返回一个监听生命周期的ID，此ID会自增\+1。当超过监听上限数量2^63\-1时，会返回\-1


 本博客参考[westworld加速](https://tianchuang88.com)。转载请注明出处！
