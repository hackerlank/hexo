---
title: iOS应用安装失败原因排查
date: 2016-05-18 21:39:16
tags: [inHouse,ios9]
---

### 在 iOS 9 中启动应用时，出现提示“未受信任的企业级开发者”

这样问题是因为在 iOS 9 以后的版本中，苹果对企业签名的应用做了更严格了限制。具体解决办法：

在 iOS 9 中，苹果对企业签名的应用运行时，进行了更严格的限制。因此，在 iOS 9 中，企业签名后的应用安装好之后，是无法直接启动的。默认情况下，在 iOS 9 中运行一款企业签名的应用时，会弹出类似这样的提示：

![a.png](https://o1wjx1evz.qnssl.com/image/view/admin_images/02f837fc3fdc37338e06374c8fdfb912)[](https://o1wjx1evz.qnssl.com/image/view/admin_images/02f837fc3fdc37338e06374c8fdfb912)[](https://o1wjx1evz.qnssl.com/image/view/admin_images/02f837fc3fdc37338e06374c8fdfb912)[](https://o1wjx1evz.qnssl.com/image/view/admin_images/02f837fc3fdc37338e06374c8fdfb912)[](https://o1wjx1evz.qnssl.com/image/view/admin_images/02f837fc3fdc37338e06374c8fdfb912)[](https://o1wjx1evz.qnssl.com/image/view/admin_images/02f837fc3fdc37338e06374c8fdfb912)[](https://o1wjx1evz.qnssl.com/image/view/admin_images/02f837fc3fdc37338e06374c8fdfb912)[](https://o1wjx1evz.qnssl.com/image/view/admin_images/02f837fc3fdc37338e06374c8fdfb912)[](https://o1wjx1evz.qnssl.com/image/view/admin_images/02f837fc3fdc37338e06374c8fdfb912)[](https://o1wjx1evz.qnssl.com/image/view/admin_images/02f837fc3fdc37338e06374c8fdfb912)[![iOS9运行企业签名应用](resources/70D395BC8A00D419754A5C910CBCF873.jpg)](https://o1wjx1evz.qnssl.com/image/view/admin_images/02f837fc3fdc37338e06374c8fdfb912)

可以看到，应用不再是像之前的版本那样直接启动，而是弹出了一个安全提示。此时，如果我们确认要运行的应用是安全的，可以按照以下步骤来设置：

在系统中打开 `设置` - `通用` - `描述文件`（在iOS 9.2以后叫：`设备管理`），此时，可以看到有一个和刚刚弹出的提示中文字类似的描述文件。然后，点击对应描述文件进入后，再点击按钮 `信任`，来让系统允许拥有这个证书的应用运行。如图所示：

![b.png](https://o1wjx1evz.qnssl.com/image/view/admin_images/2063d08973bfa64e37a5cf2d03d72b5e)[](https://o1wjx1evz.qnssl.com/image/view/admin_images/2063d08973bfa64e37a5cf2d03d72b5e)[](https://o1wjx1evz.qnssl.com/image/view/admin_images/2063d08973bfa64e37a5cf2d03d72b5e)[](https://o1wjx1evz.qnssl.com/image/view/admin_images/2063d08973bfa64e37a5cf2d03d72b5e)[](https://o1wjx1evz.qnssl.com/image/view/admin_images/2063d08973bfa64e37a5cf2d03d72b5e)[](https://o1wjx1evz.qnssl.com/image/view/admin_images/2063d08973bfa64e37a5cf2d03d72b5e)[](https://o1wjx1evz.qnssl.com/image/view/admin_images/2063d08973bfa64e37a5cf2d03d72b5e)[](https://o1wjx1evz.qnssl.com/image/view/admin_images/2063d08973bfa64e37a5cf2d03d72b5e)[](https://o1wjx1evz.qnssl.com/image/view/admin_images/2063d08973bfa64e37a5cf2d03d72b5e)[](https://o1wjx1evz.qnssl.com/image/view/admin_images/2063d08973bfa64e37a5cf2d03d72b5e)[![iOS9运行企业签名应用](resources/8E719E6E32B43DDD786C38F1C89668C8.jpg)](https://o1wjx1evz.qnssl.com/image/view/admin_images/2063d08973bfa64e37a5cf2d03d72b5e)

之后，我们就可以回到桌面，重新运行刚才的应用，就会发现应用可以正常打开了。

### 在 iOS 9 中点击“安装”按钮后，没有弹出“是否安装”的提示？

这个问题是因为 iOS 9 的一个 Bug 导致的。出现这个问题的前提，一般是由于用户已经从苹果官方 App Store 上安装了相同的应用。解决办法是：先在设备中删除之前已经安装的应用，然后再从蒲公英安装即可。

### 为什么在 iOS 9 中，点击“安装”按钮后，没有任何反应，桌面也没有出现应用图标，但是状态栏上的网络图标在转？

这是由于 iOS 9 中的一个 Bug 造成的。虽然看上去没有反应，其实应用已经在后台开始下载并安装了，状态栏上的网络图标在转就是一个证明。这个时候，只要多等待一会儿就好了，应用安装完成之后会在桌面上显示出来的。

### 在 iOS 8 或 iOS 9 中安装一个之前安装过的应用时，安装失败。

在 iOS 8 系统（或 iOS 8 以上版本）上安装应用时，有些用户可能会遇到无法安装的问题，这是因为 iOS 8（或 iOS 8 后续版本） 的一个 Bug 导致的。

修改 `plist` 文件，在其中的 `bundle-identifier` 一项中，增加一个后缀，以便 iOS 8 的设备可以正常安装应用。例如：

```
<key>bundle-identifier</key>
<string>com.mycom.MyApp</string>

```

会被修改为类似如下结果：

```
<key>bundle-identifier</key>
<string>com.mycom.MyApp.37278104</string>

```

安装时，正在安装的应用程序，会作为一个新的图标出现，当安装完成后，新的程序会自动覆盖旧的程序。

该功能仅适用于 iOS 8 （或 iOS 8 以上版本）的设备。

### 安装 iOS 应用时，出现提示“无法连接到 ssl.pgyer.com”

这个问题一般是由于用户的网络，或者手机缓存错误造成的，可以尝试如下两个方法来解决：

* 重启手机，然后尝试重新安装。
* 换一个网络环境，例如换一个 Wi-Fi 热点，或由 Wi-Fi 换成 3G/4G 等，然后重新安装。

### 其他一些可能导致应用无法安装的原因：

原因一：在导出 iOS App 的安装包文件（`.ipa`文件）时，选择了 App-Store 方式。

在导出 iOS 的 `.ipa` 文件时，有些开发者选择了 App-Store 方式，这种方式导出的 `.ipa` 文件，只适合于上传到苹果 App Store，并不能通过蒲公英来安装。如果是这种方式导出的 `.ipa`文件，传到蒲公英上时，蒲公英会显示“App-Store版”，这种版本是不能通过蒲公英安装的。

原因二：在导出 iOS App 的安装包文件（`.ipa`文件）时，选择了 Ad-hoc 方式，但是没有添加设备 UDID。

在导出 iOS 的安装包文件时，如果选择了 Ad-hoc 方式（一般用于苹果个人开发者账户），那么，如果要某台设备可以安装，则必须要将这台设备的 UDID 添加到导出安装包时所用的证书文件中（`. mobileprovision`文件），才可以在这台设备上安装。

原因三：在导出 iOS App 的安装包文件（`.ipa`文件）时，选择了 In-house 方式，但是证书已过期。

在导出 iOS 的安装包文件时，如果选择了 In-house 方式（一般用于苹果企业开发者账户），此时，如果出现无法安装的情况，开发者可以检查一下自己的企业开发者证书是否已过期。因为苹果对于企业开发者证书管理较为严格，所以开发者如果使用不当，可能会导致企业证书被封，被封后的企业证书导出的安装包，也是无法正确安装的。

原因四：开发者在生成App安装包时，没有在 Xcode 中设置正确的 Architecture。

iOS 应用的 Architecture（架构），决定了这款 iOS 应用可以在哪些设备机型上安装。例如，如果某个应用在 Xcode 中只添加了`arm64` 这一种 Architecture，那么最终打包后的安装包文件上传到蒲公英后，对于 iPad mini、iPhone5 等以下设备，都是无法安装的（因为这些设备都不是 `arm64` 架构）。换句话说，如果需要在某个设备上可以安装，App 就必须支持那个设备的 Architecture。

所以，正确的解决方法是，在生成 App 安装包时，尽可能让 App 支持更多的 Architecture。

具体操作方法是：在 `Xcode - Build Settings - Architecture` 中，增加 `armv7`、`armv7s`、`arm64`，以便所有设备都可以安装。然后，将 `"Build active architecture only"` 设置为 `NO`。

原因五：App 支持的 iOS 系统版本，和当前设备系统版本不符。

App 支持的 iOS 系统版本过低或者过高，都可能导致 App 无法安装成功。例如，如果某个 App 设置了只支持 iOS 7.0 以上的系统时，那么，如果在 iOS 6.1 系统上安装时，肯定是无法安装成功。

因此，解决的方法也很简单，我们应该尽量让 App 尽可能支持更宽泛的系统版本。

具体操作方式是：在 `Xcode` - `General` - `Deployment Info` - `Deployment Target` 中，给 App 设置一个尽量低的版本，例如 iOS 5.0。

原因六：开发者上传的是一个破解的 ipa 安装包，或者是一个使用破解 Xcode 方式打包生成的 ipa 安装包，或者是通过 iTunes 生成的 ipa 安装包。

通过任何非 Xcode（或 Xcode 的命令行工具）生成的安装包，都是没有办法正确在设备上安装的（越狱设备除外）。

正确的方法是，使用一个正常的苹果开发者证书，通过未破解的 Xcode 打包生成 ipa 安装包。

原因七：设备上已经安装了这个App，且已经安装的 App 和要安装的 App 是用不同证书打包的。

这种情况下，也会造成 App 安装失败。解决的方式很简单，开发者只需将设备上原来已经安装的 App 删除，再重新安装新的 App 即可。

原因八：`Info.plist` 文件中的`LSRequiresIPhoneOS` 没有设置，或者设置了 `NO`。

对于 iOS 的 App 来说，如果`Info.plist` 文件中的`LSRequiresIPhoneOS` 没有设置，或者设置了 `NO`，那么由 Xcode 导出的安装包（`.ipa` 包），就不会包含 `Payload` 文件夹，而是被一个叫做 `Applications` 的文件夹代替。这样的安装包在安装时，会被 iOS 判定为无效的安装包，所以无法被正确安装。

解决方式也很简单，只需要将`Info.plist` 文件中的`LSRequiresIPhoneOS` 设置为 `YES`，然后重新打包即可。具体操作为：在 Xcode 中打开 `Info.plist` 文件，然后检查 `LSRequiresIPhoneOS` 是否已设置，如果没有设置，就添加一个，然后将`LSRequiresIPhoneOS` 的类型设置为 `Boolean`，值设置为 `YES`。

设置好以后，可以看到 `Info.plist` 文件中显示 `Application requires iPhone environment` 的值为 `YES`。

原因九：网络出现中断或异常。

遇到这种情况，用户可检查自己手机的所连接的网络是否稳定、速度是否正常等。可以尝试一下其他网站，或者更换一个 Wi-Fi，或者由 Wi-Fi 换成 3G/4G 等，然后重新安装。

用这样的方式尝试后，一般都可以解决问题。
