# 10/23

妈的感觉新手村大作业做不完了，周末狂玩，毕设没做，想死捏。

20:54

今天搞了一天SubSurface的部分，不知道为什么就是没效果。

回家以后要再检查以下部分：

- GBuffer写入次表面颜色成功没？
- SubSurface宏进了没？
- ShadingModels.ush里，次表面的算法写对了没？

# 10/24

编译了几遍所有shader以后，次表面又work了。

但是自阴影和shadowmap阴影之间存在2级过渡，挺奇怪的。而且开了次表面以后，阴影变得有非常多锯齿。不知道是不是我在GetDynamicLighting里面把Attenuation写坏了。有点伤脑筋咱就是说。

# 10/25

又改了一下Attenuation的算法，依然没有改观。

今天看了一万个帖子，发现只要是VSM阴影都存在破碎的问题，不管是知乎文章还是Bili Show Reel，无一幸免。修改为普通SM或是光线追踪可以解决，SM我编译了半天引擎直接卡死了，光线追踪貌似直接不支持。

发现卡渲常见的做法中，保留真实Shadowmap阴影的本就不多，一般都是算出来的假阴影。而且SDF现在几乎是必选项，用Shadowmap根本没法做。

因此决定！！基本上彻底抛弃Shadowmap阴影！！！杀杀杀！Ramp一切！！高光Ramp、阴影身体Ramp+脸部SDF、皮肤伪3S也Ramp！

虽然不能用UE自带的次表面色有点难过啊啊啊。而且得想想那么多图要怎么传？开Pin吗还是用Project Setting传？好像都可以。感谢上周的那篇扫盲文章，不管哪种办法我都不至于无从下手。