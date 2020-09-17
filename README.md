# Using-P4-to-realize-NDN
关于使用NDN实现P4的代码目前主要有两个：
# NDN.p4
一个是signorello使用P4_14语言写的NDN.p4项目，这个主要是依靠mini-ndn（一款使用mininet生成运行nfd的host）
这里主要依靠mini-ndn来生成consumer以及producer，然后使用mini-ndn建立host与p4交换机之间的连接，在p4交换机上运行ndn.p4的p4程序，这个项目的地址
是https://github.com/signorello/NDN.p4，但是依照README中的相关步骤进行复现时会出现很多问题，比如很多程序如p4c，mini-ndn都是在不断更新的，但是这
个项目就一直没有维护，所以如果按照他的步骤安装相关程序的话就会产生很多问题，不能复现。我把当时复现这个代码的相关步骤写在了笔记里，地址是
文档：ndn.p4安装步骤.note
链接：http://note.youdao.com/noteshare?id=487f1daa3f6244a2e190b74b0e5add9f
# NDN.p4_16
第二个是netx-ulx使用p4_16语言写的NDN.p4_16项目，这个是依靠p4apprunner（一个脚本，需要在脚本中指定p4编译器、bmv2等的位置，然后传入拓扑、p4程序等
相关内容，可以直接生成相关p4交换机的拓扑，本质上还是利用的mininet），项目的地址是https://github.com/netx-ulx/NDN.p4-16/tree/master/TARGET_bmv2-ss
这个项目的论文是Named Data Networking with Programmable Switches，复现的相关步骤是：
1、必须安装mininet，我的版本是2.2.1，不能保证其他版本能够成功复现
2、克隆存储库https://github.com/p4lang/tutorials/tree/sigcomm_17。确保你能进行这些练习，并且一切都运行良好。主要的问题应该是p4apprunner.py的p4c以及bmv2
的路径存在问题，必须将第118行更改为指向p4c-bm2-ss可执行文件的位置，在第187行，替换'simple_switch'使其指向BMv2存储库可执行文件。
3、将上述https://github.com/netx-ulx/NDN.p4-16/tree/master/TARGET_bmv2-ss文件夹复制到exercise目录中，后续步骤可以参考README中
4、可能遇到的问题：一个是错误的枚举类型与定义不匹配，有些代码是错误的FixedLengthParser.p4，第33、49行等，需要进行修改，二Ingress.p4中有些action的名字重复，如、
ShiftToRightmostRaisedBit，按照p4的相关语法应该是可以的，但是名字重复导致可以正常编译但是bmv2不能正常运行，需要进行重命名。
我目前能够想到的就是这些，老师同学们在复现的过程中还有相关问题的话，请跟我联系。
